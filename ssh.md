#### Generownie klucza prywatnego/publicznego

ssh-keygen -t rsa

domyślnie zachowa w `/home/user/.ssh/id_rsa[.pub]`

Kopiowanie kluczas publicznego na zdalny serwer (serwer zapyta nas o autentykacje):
```
ssh-copy-id -i ~/.ssh/mykey user@host
```
Ręczne dopisywanie klucza publicznego do kluczy autoryzowanych na serwerze:
```
cat upload_key.pub >> ~/.ssh/authorized_keys
```