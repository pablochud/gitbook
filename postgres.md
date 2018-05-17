##### Dumping bazy

dumping tabeli django\_content\_type

`pg_dump -d toolsv4_firmy -U toolsv4 -t django_content_type > /tmp/django_content_type.sql`

##### Załadowanie bazy danymi z dumpingu

`psql toolsv4_firmy < /tmp/django_content_type.sql`

##### Stworzenie Użytkownika

`createuser -D -S -r toolsv5`  
gdzie:  
D - brak możliwości tworzenia baz  
S - nie jest superuserem  
r - Możliwość tworzenia ról

##### Stworzenie bazy

`createdb -T <szablon> -O <właściciel> <nowa_baza>`  
_\(np. createdb -T toolsv4 -O toolsv5 toolsv5\)_

##### Zmiana hasła dla użytkownika

`SQL> alter user toolsv4 with password 'toolsv4';`

```
pozwól użytkownikowi toolsv4 się połączyć lokalnie (w pg_hba.conf)::
- local toolsv4 toolsv4 md5
```