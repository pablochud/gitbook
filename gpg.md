Sciągnięcie klucza publicznego z sewera:
`gpg --keyserver pgp.mit.edu --search-keys pawel.chudziak@mga.com.pl`

`gpg --keyserver pgp.mit.edu --recv-keys <id_klucza>`

Wysłanie klucza publicznego do serwera:
`gpg --keyserver pgp.mit.edu --send-key <id_klucza>`

Zakodowanie pliku kluczem:
`gpg -o <plik_wyjsciowy> -r <podanie_klucza> -e <plik_do_enkrypcji>`

Odkodowanie pliku:
`gpg -d <plik.gpg>`

eksport klucza do pliku:
`gpg --export -a <podany_klucz> > public.key`

gpg --list-secret-keys
gpg -k