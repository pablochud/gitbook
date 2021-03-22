##### Dumping bazy

 `pg_dumpall -c -U <user_name> > dump.sql`

dumping tabeli django\_content\_type

`pg_dump -d toolsv4_firmy -U toolsv4 -t django_content_type > /tmp/django_content_type.sql`

##### Załadowanie bazy danymi z dumpingu

`cat dump.sql | docker exec -i postgres psql -U postgres`

`psql toolsv4_firmy < /tmp/django_content_type.sql`

##### Stworzenie Użytkownika

`createuser -D -S -r toolsv5`  
gdzie:  
D - brak możliwości tworzenia baz  
S - nie jest superuserem  
r - Możliwość tworzenia ról

##### Stworzenie bazy

`docker exec --user postgres -i postgres createdb <new_database_name>`

`createdb -T <szablon> -O <właściciel> <nowa_baza>`  
_\(np. createdb -T toolsv4 -O toolsv5 toolsv5\)_
stworzy tak naprawdę kopie bazy toolsv4 wraz z kontami użytkowników
czystą bazę z podstawową strukturą przygotowaną przez postgress wywołać należy przez szablon **template0**

po skopiowaniu bazy z **toolsv4** właścicielem wszystkich istniejących tabel jest "toolsv4", należy to zmienić po przez:

`SQL> REASSIGN OWNED BY <oldusername> TO <newusername>;`
opcjonalnie (jeśli baza stworzona od zera):
`SQL> GRANT ALL PRIVILEGES ON DATABASE <dbname> to <username>;`

##### Zmiana hasła dla użytkownika

`SQL> alter user toolsv4 with password 'toolsv4';`

```
pozwól użytkownikowi toolsv4 się połączyć lokalnie (w pg_hba.conf)::
- local toolsv4 toolsv4 md5
```



