# GIT
#### Usuwanie gałęzi
gałąź zdalna:
```
git push origin --delete <branch_name>
```
usuwanie lokalnych gałęzi:
```
git branch -d <branch_name>
git branch -D <branch_name> (usuwa bez pytania)
```
usuwanie śledzenia (trackingu) gałęzi nieistniejących:
```
git fetch origin --prune
```
wymuszenie aktualizacji repo zdalnego
```
git remote update origin --prune
```
Odczepienie wiązań branchy już nieinstiejących w zdalnym repo
```
git remote prune origin 
```
Usuwanie branch'y już nieaktulanych z lokalnego repo, wpier wykonać należy powyższą metodę
```
git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -D
```
Ustawienie powyższczego rozwiązania jako alias w globalnego konfiguracji. Plik `~/.gitconfig`
```
[alias]
        cleanb = !sh -c \"git branch -vv\" | grep \"origin/.*: gone]\" | awk '{print $1}' | xargs git branch -D
```