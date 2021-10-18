## Aktualizacja zmian w supervisorze

1. Dokonujemy zmian w pliku konfiguracyjnym dla jakiejś usługi
2. Nastepnie ładujemy nowe zmiany
`supervisorctl reread`
3. Wykonujemy update. Supervisord sam zresetuje usługi, które tego wymagają
`supervorctl update`

