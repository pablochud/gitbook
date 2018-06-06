```
ldapsearch -x -h 192.168.1.46  \

-D "uid=imie.nazwisko,ou=People,dc=mga,dc=com,dc=pl" \
-W     -b "ou=People,dc=mga,dc=com,dc=pl"  \
-s sub "(cn=*Ożarowski*)"
```

h to adres serwera  
D to bind name \(czyli kto pyta\)  
cn to common name
-b to w jakiej gałęzi drzewa szukanie będzie

##### Inaczej:

ldapsearch -h 10.11.3.11  -D "svc.ldap.jsp@bzmw.gov.pl" -W -b "DC=bzmw, DC=gov, DC=pl" "\(&\(sn=Tadeja\)\)" \| grep -i jsp

### LDAP Expiring Passwords

```python
#!/usr/bin/env python3

import datetime
import time
from pprint import pprint
from ldap3 import Server, Connection, SEARCH_SCOPE_WHOLE_SUBTREE

USER = "myusername"
PASS = "mypassword"
BASEDN = "OU=Users,DC=local"
SERVER = Server("127.0.0.1", port=389)
ATTRIBUTES = ['mail', 'pwdLastSet']


def construct_filter(wintimestamp):
    return """(&
       (objectCategory=Person)
       (objectCategory=User)
       (userAccountControl=512)
       (pwdLastSet<={wintimestamp})
       (mail=*)
    )""".format(wintimestamp=wintimestamp)


def search(filter):
    with Connection(SERVER, user=USER, password=PASS) as c:
        c.search(BASEDN, filter, SEARCH_SCOPE_WHOLE_SUBTREE,
                 attributes=ATTRIBUTES)
        return [record['attributes'] for record in c.response]


def datetime_to_mstimestamp(date):
    """
    Active Direcotry has different approach to create timestamp than Unix.
    Here's a function to convert the Unix timestamp to the AD one.

    >>> datetime_to_mstimestamp(datetime.datetime(2000, 1, 1, 0, 0))
    125911548000000000
    """
    timestamp = int(time.mktime(date.timetuple()))
    magic_number = 116444736000000000
    return timestamp * 10000000 + magic_number


def mstimestamp_to_datetime(mstimestamp):
    """
    Active Direcotry has different approach to create timestamp than Unix.
    Here's a function to convert AD timestamp to the Unix one.

    >>> mstimestamp_to_datetime(130567328471235643)
    datetime.datetime(2014, 10, 2, 16, 14, 7, 123563)
    """
    magic_number = 11644473600
    return datetime.datetime.fromtimestamp(
        mstimestamp / 10000000 - magic_number)


def month_ago(date):
    """
    >>> month_ago(datetime.datetime(2000, 1, 31, 0, 0))
    datetime.datetime(2000, 1, 1, 0, 0)
    """
    return date - datetime.timedelta(days=30)


def print_users_with_expiring_password():
    now = datetime.datetime.now()
    expiration_date = month_ago(now)
    wintimestamp = datetime_to_mstimestamp(expiration_date)
    older_than_month_ago = construct_filter(wintimestamp)

    for user in search(older_than_month_ago):
        user['pwdLastSet'] = mstimestamp_to_datetime(
            int(user['pwdLastSet'][0]))
        pprint(user)


if __name__ == "__main__":
    print_users_with_expiring_password()
```

### Przykład interefejsu Ldap
```python
from django.conf import settings
from django.contrib.auth import get_user_model
from ldap3 import Server, Connection


class Ldap(object):
    """ interfejs do Active Directory """

    def __init__(self, attributes=None, *args, **kwargs):
        super(Ldap, self).__init__(*args, **kwargs)
        self.server = Server(settings.AD_ADDR)
        self.userModel = get_user_model()
        if attributes:
            self.attributes = attributes
        else:
            self.attributes = ['memberof', 'objectclass', 'userPrincipalName', 'mail', 'givenName',
                               'sn', 'manager', 'telephoneNumber', 'info', 'departament']

    def utworz_lub_zaktualizuj_usera(self, username):
        """ tworzy użytkownika lub aktualizuje jego dane, jeśli taki już istnieje """
        username = username.lower()
        if settings.AD_PRINCIPAL_DOMAIN not in username:
            username = username + settings.AD_PRINCIPAL_DOMAIN
        entry = self.wyszukaj_nazwe(username)
        try:
            user = self.userModel.objects.get(username=username)
        except self.userModel.DoesNotExist:
            user = self.userModel()
            user.username = username
            user.zdalny = True

        if not user.zdalny:
            raise Exception(u'tylko dla użytkowników zdalnych')

        if not entry:
            if user.id:
                user.is_active = False
                user.save()
                return user
            else:
                raise Exception(u'nie znaleziono uzytkownika')

        if 'mail' in entry:
            user.email = entry.mail.value
        if 'givenName' in entry:
            user.first_name = entry.givenName.value
        if 'sn' in entry:
            user.last_name = entry.sn.value
        if 'telephoneNumber' in entry:
            user.telefon = entry.telephoneNumber

        if 'departament' in entry:
            user.wydzial = entry.departament.value
        elif 'info' in entry:
            user.wydzial = entry.info.value

        user.save()
        return user

    def w_grupach(self, grupy_usera):
        """ sprawdza czy użytkownik jest w wszystkich podanych grupach """
        for wymagana_grupa in settings.AD_REQ_GRPS:
            if wymagana_grupa not in grupy_usera:
                return False
        return True

    def wyszukaj_usera(self, zapytanie, size_limit=None, filtruj_grupy=True):
        """ wyszukiwanie obób w AD """
        grupy = ''
        if filtruj_grupy:
            for wymagana_grupa in settings.AD_REQ_GRPS:
                grupy = grupy + '(memberof={0})'.format(wymagana_grupa, )
        zapytanie_glowne = '( &(objectclass=person)({0}){1} )'.format(zapytanie, grupy)
        if not size_limit:
            size_limit = 10
        if settings.AD_PASS is None or settings.AD_PASS.strip() == '':
            raise ValueError('''
                -------------------------------------------------------------------
                      Musisz ustawić zmienną AD_PASS z hasłem użytkownika LDAP
                -------------------------------------------------------------------
                ''')
        conn = Connection(self.server, user=settings.AD_USER, password=settings.AD_PASS, auto_bind=True)
        conn.search(settings.AD_BASE_DN, zapytanie_glowne,
                    attributes=self.attributes, size_limit=size_limit)
        entries = conn.entries
        return entries

    def wyszukaj_nazwe(self, nazwa, filtruj_grupy=True):
        """ wyszukiwanie po loginie: exact"""
        if settings.AD_PRINCIPAL_DOMAIN not in nazwa:
            nazwa = nazwa + settings.AD_PRINCIPAL_DOMAIN
        res = self.wyszukaj_usera('userPrincipalName={0}'.format(nazwa), filtruj_grupy=filtruj_grupy)
        if len(res) == 1:
            return res[0]
        return None

    def wyszukaj_in(self, slowa_kluczowe):
        """ wyszukiwanie po imieniu, nazwisku i loginie: like """
        slowa = slowa_kluczowe.split(' ')
        if len(slowa) == 1:
            return self.wyszukaj_usera('| (cn=*{0}*) (userPrincipalName=*{0}*)'.format(slowa[0], ))
        elif len(slowa) > 1:
            return self.wyszukaj_usera(
                '| (&(givenName={0}*)(sn={1}*)) (&(givenName={1}*)(sn={0}*))'.format(slowa[0], slowa[1]))
        else:
            return None
```
