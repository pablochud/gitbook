Otworzenie loga systemu:  
`:/var/log$ dmesg`  
Sprawdzenie zainstalowanych pakietów na przykładzie "network-manager-openvpn":  
`sudo apt-cache search network-manager-openvpn`

date +%s \| sha256sum \| base64 \| head -c 32; echo  
date \| md5sum

while true; do \(echo "%CPU %MEM ARGS $\(date\)" && ps -e -o pcpu,pmem,args --sort=pcpu \| cut -d" " -f1-5 \| tail\) &gt;&gt; ps.log; sleep 5; done

grep -iE '^od\_faktury\|\[\[:space:\]\]od\_faktury' -r forms/

