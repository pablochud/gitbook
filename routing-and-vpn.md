#### Routing
Badanie trasy pakietów w sieci IP:
(Wysyłany jest pakiet w celu określenia informacji na temat kolejnych routerach)
`traceroute google.pl`
Tablica trasowaania pakietów sieciowych:
`route`
Usuwanie pozycji z tablicy trasowania:
`ip route del default via 192.168.43.1`
Dodawanie pozycji do tablicy trasowania i ustawianie metryki: 
(im mniejsza metryka tym większy priorytet)
`ip route add default via 192.168.43.1 metric 40`
> W trakcie połączenia z VPN możesz nie mieć dostępu do internetu, co może być spowodowane tym, że routing połaczenia internetowego jest ustawiony na, w roli pośrednika, maszynę z VPN. Dzieje się tak ponieważ odpowiedzialne za to trasowanie ma wyższą metryke - należy wówczas zmienić metrykę odpowiedniego trasowania.

#### VPN
