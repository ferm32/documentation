## Polib - a library to manipulate gettext (po and mo) files.
Актуализировано для polib 1.03 (2013/02/09)

Примечание. Сокращены сведения о манипуляциях с mo-файлами.

[Polib in PyPI packages index](https://pypi.python.org/pypi/polib)


### Загрузка po каталога с указанием кодировки

    import polib
    po = polib.pofile(
        'path/to/catalog.po',
        encoding='iso-8859-15'
    )

### Создание po каталога с нуля

    import polib
    
    po = polib.POFile()
    po.metadata = {
        'Project-Id-Version': '1.0',
        'Report-Msgid-Bugs-To': 'you@example.com',
        'POT-Creation-Date': '2007-10-18 14:00+0100',
        'PO-Revision-Date': '2007-10-18 14:00+0100',
        'Last-Translator': 'you <you@example.com>',
        'Language-Team': 'English <yourteam@example.com>',
        'MIME-Version': '1.0',
        'Content-Type': 'text/plain; charset=utf-8',
        'Content-Transfer-Encoding': '8bit',
    }

Этот фрагмент создаёт пустой файл po с указанными метаданными, теперь можно добавлять записи к файлу следующим образом:

    entry = polib.POEntry(
        msgid=u'Welcome',
        msgstr=u'Bienvenue',
        occurrences=[('welcome.py', '12'), ('anotherfile.py', '34')]
    )
    po.append(entry)

Для сохранения файла на диск необходимо сделать:

    po.save('/path/to/newfile.po')

### Ещё примеры
#### Перебрать все записи
    import polib
    
    po = polib.pofile('path/to/catalog.po')
    for entry in po:
        print entry.msgid, entry.msgstr
#### Перебрать все записи, кроме устаревших
    import polib
    
    po = polib.pofile('path/to/catalog.po')
    valid_entries = [e for e in po if not e.obsolete]
    for entry in valid_entries:
        print entry.msgid, entry.msgstr
#### Перебрать только переведённые записи
    import polib
    
    po = polib.pofile('path/to/catalog.po')
    for entry in po.translated_entries():
        print entry.msgid, entry.msgstr

Также можно исползовать другие методы объекта POEntry:

- untranslated_entries()
- fuzzy_entries()

#### Подсчитать процент переведённых записей
    import polib
    
    po = polib.pofile('path/to/catalog.po')
    print po.percent_translated()


#### Функция `escape`

    polib.escape(st)[source]

Escapes the characters \\, \t, \n, \r and " in the given string st and returns it.

#### Функция `unescape`

    polib.unescape(st)[source]

Unescapes the characters \\, \t, \n, \r and " in the given string st and returns it.



