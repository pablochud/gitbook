
##### Dumping bazy
dumping tabeli django_content_type

`
pg_dump -d toolsv4_firmy -U toolsv4 -t django_content_type > /tmp/django_content_type.sql
`
##### Załadowanie bazy danymi z dumpingu
`psql toolsv4_firmy < /tmp/django_content_type.sql`

