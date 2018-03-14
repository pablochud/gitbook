w
hile true; do (echo "%CPU %MEM ARGS $(date)" && ps 
-e -o pcpu,pmem,args --sort=pcpu | cut -d" " -f1-5 |
tail) > ps.log; sleep 5; doneOtworzenie loga systemu:  
`:/var/log$ dmesg`  
Sprawdzenie zainstalowanych pakietów na przykładzie "network-manager-openvpn":  
`sudo apt-cache search network-manager-openvpn`

### Generowanie randomych haseł

przykład generowania haseł za pomocą bieżącej daty i szyfrowania  
`date +%s | sha256sum | base64 | head -c 32; echo`   
`date | md5sum`

### Logowanie procesów do pliku


while true; do (echo "%CPU %MEM ARGS $(date)" && ps -e -o pcpu,pmem,args --sort=pcpu | cut -d" " -f1-5 | tail) > ps.log; sleep 5; done


### Grepowanie z wyrażeniami regularnymi

grep -iE '^od\_faktury\|\[\[:space:\]\]od\_faktury' -r forms/

### Format wyświetlania historii komend

`HISTTIMEFORMAT="%d/%m/%y %T "`  
 `echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile`  
 następnie trzeba załadować zmodyfikowany plik do obecnego terminala

