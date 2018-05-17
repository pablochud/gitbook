# Posługiwanie się narzędziem TAR

utworzenie archiwum:

```
tar -czvf <file_name>.gz /path/to/file
```

J to --xz

```
tar cJf <file_name>.xz /path/to/file
```

wypakowanie archiwum:

```
tar -xzvf <file_name>.gz
tar -xzvf <file_name>.gz -C /tmp/
```

albo po prostu

```
tar xf initial_fixtures.tar.xz
```



