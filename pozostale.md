while true; do \(echo "%CPU %MEM ARGS $\(date\)" && ps  
-e -o pcpu,pmem,args --sort=pcpu \| cut -d" " -f1-5 \|  
tail\) &gt; ps.log; sleep 5; doneOtworzenie loga systemu:  
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





select DBMS_METADATA.GET_DDL (
object_type     => 'PACKAGE',
name            => 'DEKL_IMPORT',
schema          => 'F_JSP')
from dual;

ldapsearch -x -h 192.168.1.46  \
-D "uid=robert.wieczorek,ou=People,dc=mga,dc=com,dc=pl" \
-W     -b "ou=People,dc=mga,dc=com,dc=pl"  \
-s sub "(cn=*Ożarowski*)"