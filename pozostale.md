### Uprawnienia użytkownika do wywoływania komend bez sudo

uruchomić komendę `visudo`

```bash
# Cmnd alias specification
Cmnd_Alias RESTART_EBOK_DEVEL = /usr/local/bin/supervisorctl restart dev\:toolsv4gunicorn_dev

# User privilege specification
root    ALL=(ALL:ALL) ALL
toolsv4dev ALL=(ALL) NOPASSWD: RESTART_EBOK_DEVEL
```

### Szukanie paczek zainstalowanych

Otworzenie loga systemu:  
`:/var/log$ dmesg`  
Sprawdzenie zainstalowanych pakietów na przykładzie "network-manager-openvpn":  
`sudo apt-cache search network-manager-openvpn`

### Generowanie randomych haseł

przykład generowania haseł za pomocą bieżącej daty i szyfrowania  
`date +%s | sha256sum | base64 | head -c 32; echo`  
`date | md5sum`

### Logowanie procesów do pliku

while true; do \(echo "%CPU %MEM ARGS $\(date\)" && ps -e -o pcpu,pmem,args --sort=pcpu \| cut -d" " -f1-5 \| tail\) &gt; ps.log; sleep 5; done

### Grepowanie z wyrażeniami regularnymi

grep -iE '^od\_faktury\|\[\[:space:\]\]od\_faktury' -r forms/

### Format wyświetlania historii komend

`HISTTIMEFORMAT="%d/%m/%y %T "`  
 `echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile`  
 następnie trzeba załadować zmodyfikowany plik do obecnego terminala

### Usuwanie plików z zapisanej listy
Listę plików zapisać możemy jako:
`ls -1 > lista.txt`
następnie wykorzystać pętle:
```bash
for f in $(cat 1.txt) ; do 
  rm "$f"
done
```
albo:
```bash
xargs rm -rf < 1.txt
```

### ----------

select DBMS\_METADATA.GET\_DDL \(  
object\_type     =&gt; 'PACKAGE',  
name            =&gt; 'DEKL\_IMPORT',  
schema          =&gt; 'F\_JSP'\)  
from dual;

ldapsearch -x -h 192.168.1.46  \  
-D "uid=robert.wieczorek,ou=People,dc=mga,dc=com,dc=pl" \  
-W     -b "ou=People,dc=mga,dc=com,dc=pl"  \  
-s sub "\(cn=_Ożarowski_\)"

