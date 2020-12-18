#### PIP
Podanie źródła paczek
```
pip install --no-index --find-links ./nowy/ -r ./nowy/requirements.txt
pip install <paczka> --no-index --find-links <path>
```
`--find-links`: podaje ścieżke, w której znajdzie paczki

`--no-index`: szukaj jedynie w ścieżce podanej w *--find-links*

* **Dla nowszych wersji pip ściąganie paczek:**
```
pip download <paczka> -d <path>
pip download -r requirements.txt
pip download <paczka> --no-binary=:all:
```
`-d`: wskazuje na ścieżke do której pobrać paczke

`--no-binary`: pobiera zarchiwizowane paczki i wszystie ich zależności

* **W starszych wersja skruktura polecenia wygląda:**
```
pip install <paczka> --download="<path>" --no-use-wheel
```
`--download`: określa, że chcemy ściągnąć paczke, jak ścieżke, w której chcemy ją zapisać.

`--no-use-wheel`: określa, że nie chcemy pobierać w formie whl, pobierze jako tar.

pip freeze > requirements.txt

#### Virtualenv - przygotowanie innych wersji pip
```
virtualenv -p /usr/bin/python3.4 <envname>
virtualenv -p python3.4 <envname>
virtualenv -p python3.4 --no-pip <envname>
```
`--no-pip`: utworzenie wirtualnego środowiska bez instalacji pip na nim

uruchomienie środowiska
```
source <envname>/bin/active
```

możliwość zainstalowanie konkretnej wersji pip
```
pip install pip==9.0.1
```

### Test
Nie testowałem, ale jest takie rozwiązanie
```
python -m pip download \
   --only-binary=:all: \
   --platform any \
   --python-version 3 \
   --implementation py \
   SomePackage
```

* **Przerzucanie paczek**

Paczki najlepiej przesyłać `rsync` zamiast `scp`
```
rsync -rvz -e 'ssh -p <port>' --progress ./whl root@<host>:/tmp
```
