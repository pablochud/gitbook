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

