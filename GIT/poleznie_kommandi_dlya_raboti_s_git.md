# Полезные комманды для работы с git

сбросить мастер

```
git reset --hard origin/master
```

сбросить мерж

```
git merge --abort
```

отменить последний корммит

```
git reset --soft HEAD~1
```

Команда для того чтобы удалить все смерженые(–merged) ветки за исключением текущей(-v ‘*’):

```
git branch --merged | grep -v '*' | xargs git branch -D
```

Инициализировать репозиторий в текущей папке

```
cd <localdir>
git init
git add .
git commit -m 'init'
git remote add origin url
git push -u origin master
```