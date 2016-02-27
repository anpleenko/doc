#Примеры GIT

1. Склонировать репозиторий без истории

    ```
    $ git clone --depth 1 https://github.com/Bubujka/ru.najomi.org-data.git
    ```

1. Сделать экспорт (аля svn export) ветки мастер в другую папку:

    ```
    $ git archive master | tar -x -C /somewhere/else
    ```

1. Клонировать репозиторий

    ```
    $ git clone ssh://user@somehost:port/~user/repository
    $ git clone git://user@somehost:port/~user/repository/project.git
    $ git clone http://user@somehost:port/~user/repository/project.git
    $ git clone file:///home/username/project myrepo

    # Этот вариант отличается от того, что начинается с file://
    # Он работает быстрее, но утягивает заметно больше информации.
    $ git clone /home/username/project myrepo
    ```

1. Редактировать конфиг в редакторе по умолчанию. Если не задан параметр --global, то редактируется .git/config, иначе ~/.gitconfig

    ```
    $ git config -e [--global]
    ```

1. Добавить удаленный репозиторий

    ```
    $ git remote add bob /home/bob/myrepo
    ```

1. Удалить файл из комита и с жесткого диска

    ```
    $ git rm -f file1 file2 ... fileN
    ```

1. Отменить все изменения, сделанныe в дереве, до состояния, которое было при последнем commit в локальный репозиторий

    ```
    $ git reset --hard
    ```

1. Удалить из индекса конкретный файл

    ```
    $ git reset - EDITEDFILE
    ```

1. Удалить из папки документации к git все файлы txt

    ```
    $ git rm Documentation/\*.txt
    ```

1. Навсегда удалить три последних коммита

    ```
    $ git reset --hard HEAD~3
    ```

1. Отменить коммит

    ```
    $ git revert config-modify-tag
    $ git revert cgsjd2h
    ```

1. Просмотреть содержимое определённого коммита

    ```
    $ git show d028769

    commit d028769abbdcfa3e6cdba76cb1d6b569e5afe88e
    Author: Aleksei Kaminin <zendzirou@gmail.com>
    Date:   Sun Aug 14 22:17:19 2011 +0400

        Adde link to _nix category

    diff --git a/_nix/meta.yaml b/_nix/meta.yaml
    index bdb05a9..b107d80 100644
    --- a/_nix/meta.yaml
    +++ b/_nix/meta.yaml
    @@ -14,3 +14,4 @@ keywords:
       - примеры bsd
     links:
       - [http://www.opennet.ru/tips/sml/, 'много интересных заметок на разные темы']
    +  - [http://www.linuxselfhelp.com/, 'большой сборник документаций']
    ```

1. Вывести информацию о том кто автор и когда менялись первые 3 строки файла README

    ```
    $ git blame -L 1,+3 README

    59246055 (Aleksei Kaminin 2011-08-04 15:00:12 +0400 1) Это репозиторий с ...
    3426e293 (Aleksei Kaminin 2011-08-04 14:59:20 +0400 2)
    3426e293 (Aleksei Kaminin 2011-08-04 14:59:20 +0400 3) Основной адрес: ht...
    ```

1. Попробовать объединить текущую ветку с веткой new_feature

    ```
    $ git merge new_feature
    ```

1. Переименовать файл bug.c в файл feature.c

    ```
    $ git mv bug.c feature.c
    ```

1. Посмотреть статистику коммитов по автору

    ```
    $ git shortlog -s -n

    118  Aleksei Kaminin
      3  Alesenko Elena
      3  Lena Omega
      3  unknown
    ```

1. Взять коммит с номером 7496f529 и применить его к текущей ветке

    ```
    $ git cherry-pick 7496f529
    ```

1. Взять правки из коммита 7496f529, применить их к текущей ветке, но сам коммит не совершать

    ```
    $ git cherry-pick -n 7496f529
    ```

1. Изменить сообщение в предыдущем коммите

    ```
    $ git commit --amend
    ```

1. Добавить изменения к предыдущему коммиту

    ```
    $ git commit --amend -a
    ```

1. Cоздать tar-архив проекта и записать его в файл ~/prj.tar. Внутри него файлы будут находится в папке proj-1.2.3/

    ```
    $ git archive --format=tar --prefix=proj-1.2.3/ HEAD > ~/prj.tar
    ```

1. Для каждой сделанной правки без коммита показать измененный участок кода и спросить, должно ли это изменение попасть в следующий коммит.

    ```
    $ git add -p
    ```

1. Рекурсивно удалить все файлы в папке "vim/insert mode"

    ```
    $ git rm -rf 'vim/insert mode'
    ```

1. Показать файл, как он выглядел коммит назад

    ```
    $ git show HEAD^:view/prj/one_example.php
    ```

1. Кунг-фу по git-clean. TL;DR git clean -fdx удалить все новые файлы, пустые каталоги, и то что попадает под действие .gitignore Ключ -n вместо -f застаяляет git clean не выполнять реальных действий по удалению.

    ```
    #Создаём репозиторий

    $ git init

    Initialized empty Git repository in /home/waserd/tmp/.git/

    $ touch a b c
    $ mkdir tmp
    $ touch tmp/lock
    $ git add .
    $ echo 'tmp/*' > .gitignore
    $ git add .
    $ git commit -m init

    [master (root-commit) bce15e8] init
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 .gitignore
     create mode 100644 a
     create mode 100644 b
     create mode 100644 c
     create mode 100644 tmp/lock

    #Вносим в него различные правки

    $ touch d tmp/{1,2,3}
    $ ls > a
    $ mkdir e
    $ touch e/f
    $ git status

    # On branch master
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   a
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #       d
    #       e/
    no changes added to commit (use "git add" and/or "git commit -a")

    #Смотрим что удалит git clean по умолчанию

    $ git clean -n

    Would remove d
    Would not remove e/

    #Ключ -d удалит пустые каталоги заодно

    $ git clean -nd

    Would remove d
    Would remove e/

    #А ключ -x удалит всё, будто .gitignore у нас нет.

    $ git clean -ndx

    Would remove d
    Would remove e/
    Would remove tmp/1
    Would remove tmp/2
    Would remove tmp/3

    #Удаляем

    $ git clean -fdx

    Removing d
    Removing e/
    Removing tmp/1
    Removing tmp/2
    Removing tmp/3

    #Почти чисто =)

    $ git status

    # On branch master
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   a
    #
    no changes added to commit (use "git add" and/or "git commit -a")
    ```

1. Удалить из индекса все файлы, что были удалены не через git.

    ```
    $ rm b d foo/baz
    $ git status

    # On branch master
    # Changed but not updated:
    #   (use "git add/rm <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       deleted:    b
    #       deleted:    d
    #       deleted:    foo/baz
    #
    no changes added to commit (use "git add" and/or "git commit -a")

    $ git add -u
    $ git status

    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #       deleted:    b
    #       deleted:    d
    #       deleted:    foo/baz
    #
    ```

1. Создать новый "голый" репозиторий my_project.git

    ```
    $ git clone --bare my_project my_project.git

    Initialized empty Git repository in /opt/projects/my_project.git/
    ```

1. Добавить право на запись для группы в репозиторий, который находится на сервере

    ```
    $ ssh user@git.example.com
    $ cd /opt/git/my_project.git
    $ git init --bare --shared
    ```

1. Использовать графические инструменты для разрешения конфликтов при слиянии веток

    ```
    $ git mergetool

    merge tool candidates: kdiff3 tkdiff xxdiff meld gvimdiff opendiff emerge vimdiff
    Merging the files: index.html

    Normal merge conflict for 'index.html':
      {local}: modified
      {remote}: modified
    Hit return to start merge resolution tool (opendiff):
    ```

1. Открыть страницу руководства Git по команде merge

    ```
    $ git help merge
    $ git merge --help
    $ man git-merge
    ```

