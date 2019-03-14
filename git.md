# GIT
#### Squashowanie commitów
squash ostatnich 5 commitów:
```
rebase -i HEAD~5
```
squash do konkretnego commita:
```
git rebase -i <after-this-commit>
```
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
#### Mergowanie nowych zmian ze zdalnego repozytorium
z akceptacją zmian przychodzących
```
git pull -s recursive -X theirs <remoterepo>
```
#### Mergowanie z Projektu-a do Projektu-b
```
cd path/to/project-b
git remote add project-a path/to/project-a
git fetch project-a --tags
git merge --allow-unrelated-histories project-a/master # or whichever branch you want to merge
git remote remove project-a
```
`--allow-unrelated-histories parameter only exists since git >= 2.9`
`--tags in order to keep tags.`
#### Przywrócenie commita
cofnięcie do niespushowanego commita:
```
git reset HEAD~
```
zresetowanie zmian do ostatniego commita z gałęzi:
```
git reset --hard origin/test
```
