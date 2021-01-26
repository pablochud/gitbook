#### Export Public Key

This command will export an ascii armored version of the public key:
```
gpg --output public.pgp --armor --export username@email
```
```
gpg --armor --export <podany_klucz> > public.key
```

#### Export Secret Key

This command will export an ascii armored version of the secret key:
```
gpg --output private.pgp --armor --export-secret-key username@email
```

#### Sciągnięcie klucza publicznego z sewera:
```
gpg --keyserver pgp.mit.edu --search-keys pawel.chudziak@mga.com.pl
```

```
gpg --keyserver pgp.mit.edu --recv-keys <id_klucza>
```

#### Wysłanie klucza publicznego do serwera:
```
gpg --keyserver pgp.mit.edu --send-key <id_klucza>
```

#### Zakodowanie pliku kluczem:
```
gpg -o <plik_wyjsciowy> -r <podanie_klucza> -e <plik_do_enkrypcji>
```

#### Odkodowanie pliku:
```
gpg -d <plik.gpg>
```


gpg --list-secret-keys
gpg -k
