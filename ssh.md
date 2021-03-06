#### Dodanie passphrase do klucza
```
openssl rsa -aes256 -in your.key -out your.encrypted.key
```
wówczas łączymy się z serwerem
```
ssh -i [ścieżka_do_klucza] user@server
```

#### Generownie klucza prywatnego/publicznego
Tworzenie klucza w najprostrzej formie:
```
ssh-keygen -t rsa
```
Tworzenie `-o` klucza w nowszym bezpieczniejszym formacie, z większą `-b` ilością użytych bitów przy generowaniu i z powiązanym `-C` komentarzem opisującym klucz (opcjonalne)
```
ssh-keygen -o -t rsa -b 4096 -C "email@example.com"
```

domyślnie zachowa w `/home/user/.ssh/id_rsa[.pub]`

Kopiowanie kluczas publicznego na zdalny serwer (serwer zapyta nas o autentykacje):
```
ssh-copy-id -i ~/.ssh/mykey user@host
```
Ręczne dopisywanie klucza publicznego do kluczy autoryzowanych na serwerze:
```
cat upload_key.pub >> ~/.ssh/authorized_keys
```

Przejrzenie fingerprintsów kluczy można wykonań poleceniem (następnie porównać je z kluczami na gitlabie):

`-l` wylistuj zamiast generuj nowy klucz, `-f` wskazanie pliku
```
$ ssh-keygen -lf /path/to/ssh/key

```
