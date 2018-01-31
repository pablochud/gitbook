#CELERY
(Stara wersja celery z użyciem pakietu celeryd)
Uruchamianie dwóch workerów celery
`./manage.py celeryd multi start 2 -B -l info`
`./manage.py celeryd -B -E -l info --concurrency=4`


?:
`celery -A toolsv4 inspect stats`

Aktulane realizowany task w kolejce:
`celery -A toolsv4 inspect active`

Lista tasków oczekujących w kolejce:
`celery -A toolsv4 inspect reserved`
?"
`celery -A toolsv4 status`

Pozostałe:
|as|as|
|:---|:---|
|sa|sa|







