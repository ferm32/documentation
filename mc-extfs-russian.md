## Написание скриптов для внешних виртауальных файловых систем (vfs) Midnight Commander
Исходный файл: https://github.com/MidnightCommander/mc/blob/master/src/vfs/extfs/helpers/README

Стоит таже посмотреть черновик README.extfs от Adam Byrtek https://mail.gnome.org/archives/mc-devel/2002-December/msg00131.html

**ВАЖНОЕ ЗАМЕЧАНИЕ:** В extfs всё ещё могут оставаться некоторые баги. Удачи.

Начиная с версии 3.1, Midnight Commander идёт с такой штукой, как **extfs**,которая является одной из виртуальных фаловых систем. Эта система делает возможным и очень простым создание новых виртуальных файловых систем для GNU MC.

Для обработки запросов, создайте скрипт (программу) на shell, perl, python и т. п. в директории `$(libexecdir)/mc/extfs.d или в ~/.local/share/mc/extfs.d/`.

(Замечине: вместо `$(libexecdir)` следует подставить актуальны путь, заданный при конфигурировании или компиляции, например, `/usr/local/libexec` или `/usr/libexec)`.

Присвойте виртуальной ФС суффикс. Например, если у Вас .zip-файл, и Вы желаете
посмотреть, что внутри него, путь будет таким:

    /anypath/my.zip/uzip://some_path/...

В этом примере, расширение - `.zip`, но виртуальная файловая систем названа `'uzip'`. Почему? Потому то, что в сущности делает данная vfs - это UNzip. UN слишком длинно, поэтому оставлено U. Заметим, что когда-то в будущем, может появиться и файловая система с именем zip: она будет брать целую директорию и создавать из неё zip-файл. Таким образом, `/usr/zip://` -будет zip-файлом, например, с целым деревом файлов и папок внутри `/usr`.

Если Ваша vfs не требует для своей работы файлама, добавьте в конце её имени символ '+'. Заметим, что завершающий '+' в имени файла - это не часть имени vfs, это лишь атрибут vfs. Поэтому, Вы не должны его использжовать в командах vfs:

    cd rpms://

\- корректная команда, а

    cd rpms+://

\- некорректная.


### Команды, которые следует реализовать в Вашем shell-скрипте
В случае успешного выполнения команды Ваш скрипт должен вернуть ноль. В обратном случае, когда произойдёт сбой или будет запрошено выполнение неподдерживаемой команды - необходимо вернуть ненулевое значение.

    $libdir/extfs/prefix command [arguments]

#### Команда: list archivename

Данная команда должна вывести полный список содержимого архива в следующем
формате (слегка изменённый формат вывода команды ls -l):

    AAAAAAA NNN OOOOOOOO GGGGGGGG SSSSSSSS DATETIME [PATH/]FILENAME [-> [PATH/]FILENAME[/]]]

где (в квадратных скобках [] необязательная часть):

    AAAAAAA  строка разрешений, подобная той, которая выводится при ls -l
    NNN      количество ссылок (links)
    OOOOOOOO владелец (UID или имя)
    GGGGGGGG группа (GID или имя)
    SSSSSSSS размер файла
    FILENAME имя файла
    PATH     путь от корня архива без завершающего слэша (/)
    DATETIME имеет один из следующих форматов:
                Mon DD hh:mm[:ss], Mon DD YYYY, MM-DD-YYYY hh:mm[:ss]

                где Mon - три буквы из английского названия дня недели,
                DD - число 01-31 (может быть указано как 1-31, если следует на Mon),
                MM - месяц 01-12, YYYY - четырёхзначный год,
                hh - часы, mm - минуты, ss - необязательные секунды.

Если присутствует часть `-> [PATH/]FILENAME`, это означает следующее.

Если разрешения начинаются с символа `l`, то это имя, на который указывает симлинк (если PATH начинается с префикса vfs, то это симлинк на какую-либо другую виртуальную файловую систему, если Вы хотите указать путь от локального корня файловой системы, используйте `local:/path_name` вместо `/path_name`, так как `/path_name` будет означать путь от корня архива, содержимое которого выводится).

Если разрешения не начинаются с символа `l`, но число линков больше одного, то этот файл должен быть жёстко связан (hardlined) с другим файлом.

Результат команды `list` не должен содержать элементов "." и "..".

#### Команда: copyout archivename storedfilename extractto

Должна излечь из архива `archivename` файл `storedfilename` в файл `extractto`.

#### Команда: copyin archivename storedfilename sourcefile

Должна добавить `sourcefile` в архив `archivename` с именем `storedfilename`.

Important note: archivename in the above examples may not have the
extension you are expecting to have, like it may happen that
archivename will be something like /tmp/f43513254 or just
anything. Some archivers do not like it, so you'll have to find some
workaround.

#### Command: rm archivename storedfilename

This should remove storedfilename from archivename.

#### Command: mkdir archivename dirname

This should create a new directory called dirname inside archivename.

#### Command: rmdir archivename dirname

This should remove an existing directory dirname. If the directory is
not empty, mc will recursively delete it (possibly prompting).

#### Command: run

Undocumented :-)

***

Don't forget to mark this file executable (chmod 755 ThisFile, for example)

For skeleton structure of executable, look at some of filesystems
similar to yours.

***

In constructing these routines, errors will be made, and mc will not display
a malformed printing line.  That can lead the programmer down many false
trails in search of the bug.  Since this routine is an executable shell script
it can be run from the command line independently of mc, and its output will
show on the console or can be redirected to a file.

#### Putting it to use
The file .mc.ext in a home directory, and in mc's user directory (commonly
/etc/mc), contains instructions for operations on files depending
on filename extensions.  It is well documented in other files in this
distribution, so here are just a few notes specifically on use of the
Virtual File System you just built.

