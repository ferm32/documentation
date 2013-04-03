#ISPmanager_API
Второстепенные моменты опущены. Также опущены параметры, работающие только в версиях Pro и Cluster. Актуально на 03.04.2013.

Оригинал: [http://ru.ispdoc.com/index.php/ISPmanager_API](http://ru.ispdoc.com/index.php/ISPmanager_API)

###Пользователи - просмотр
Функция: **user**

Результат: список элементов

- **name** - Имя.
- **slave** - Сервер.
- **owner** - Владелец.
- **preset** - Шаблон.
- **disabled** - Учётная запись и её WWW домены временно отключены.
- **unex** - Для учетной записи не определены свойства и настройки панели.
- **cgi** - Пользователь может использовать CGI для своих WWW доменов.
- **wsgi** - Пользователь может использовать WSGI для своих WWW доменов.
- **php** - Пользователь может использовать PHP для своих WWW доменов.
- **ssi** - Пользователь может использовать SSI для своих WWW доменов.
- **ssl** - Пользователь может использовать безопасное соединение по протоколу HTTPs для своих WWW доменов.
- **shell** - Пользователь может использовать shell.
- **usermove** - Идет импорт пользователя.
- **note** - Заметки: .
- **disk** - Диск. Атрибуты :
  - **used** - Использованное количество.
  - **limit** - Максимально возможное значение. 
- **bandwidth** - Трафик. Атрибуты :
  - **used** - Использованное количество.
  - **limit** - Максимально возможное значение. 

###Пользователи - создание, изменение
Функция: **user.edit**

Данная функция одновременно используется для просмотра параметров объекта, изменения объекта и создания нового объекта.

#####Просмотр параметров объекта:
- Параметры:
  - **elid** - уникальный идентификатор (элемент "name" из функции "user")
- Результат: список параметров объекта

#####Создание объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

#####Изменение объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - **elid** - уникальный идентификатор (элемент "name" из функции "user")
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

Список параметров объекта или дополнительных параметров запроса (см.выше):

- **name** - Имя пользователя.
- **passwd** - Пароль.
- **confirm** - Подтверждение.
- **ip** - IP-адрес.
- **ip6** - IPv6-адрес. Параметр зависим от возможности **ipv6**.
- **domain** - Домен.
- **preset** - Шаблон.
- **shell** - Доступ к shell. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".)
- **ssl** - SSL. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **ssl**.
- **cgi** - CGI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **cgi**. Активный параметр разрешает следующие параметры: 'phpcgi','phpfcgi'
- **wsgi** - WSGI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **wsgi**.
- **ssi** - SSI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **ssi**.
- **phpmod** - PHP как модуль Apache. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **phpmod**.
- **phpcgi** - PHP как CGI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **phpcgi**.
- **phpfcgi** - PHP как FastCGI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **phpfcgi**.
- **disklimit** - Диск. Параметр зависим от возможности **quota**.
- **ftplimit** - FTP аккаунты. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **ftp**.
- **maillimit** - Почтовые ящики. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **email**.
- **domainlimit** - Домены. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **dns**.
- **webdomainlimit** - WWW домены. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **www**.
- **maildomainlimit** - Почтовые домены. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **email**.
- **baselimit** - Базы данных. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **db**.
- **baseuserlimit** - Пользователи баз данных. (Числовое значение. Для указания "бесконечности" используйте "10000".) Параметр зависим от возможности **db**.
- **bandwidthlimit** - Трафик. (Числовое значение. Для указания "бесконечности" используйте "100000000".)
- **cpulimit** - Ограничение на CPU. (Числовое значение. Для указания "бесконечности" используйте "100000".)
- **memlimit** - Ограничение на память. (Числовое значение. Для указания "бесконечности" используйте "100000".)
- **proclimit** - Количество процессов. (Числовое значение. Для указания "бесконечности" используйте "100000".)
- **mysqlquerieslimit** - Запросов к MySQL. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **dbhaslimits**.
- **mysqlupdateslimit** - Обновлений MySQL. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **dbhaslimits**.
- **mysqlconnectlimit** - Соединений к MySQL. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности dbhaslimits.
- **mysqluserconnectlimit** - Одновременных соединений к MySQL. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **dbhasuconnlimits**.
- **maxclientsvhost** - Воркеров apache mpm-itk. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **apache-mpm-itk**.
- **limitconn** - Одновременных соединений на сессию. (Числовое значение. Для указания "бесконечности" используйте "65535".) Параметр зависим от возможности **nginx**. Image:isp_pro.png Image:isp_cluster.png
- **mailrate** - Количество отправляемых писем. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **mailrate**.
- **note** - .

###Пользователи - удаление
Функция: **user.delete**

Параметры:
- elid - один или несколько уникальных идентификаторов объекта, разделенных запятой и следующим за ней пробелом ", ". Уникальный идентификатор - это элемент "name" из функции "user".

Результат: успешное выполнение операции или сообщение об ошибке

###Сохранение файлов пользователя
Функция: **backuponeclick**
- destdir - Каталог для архива.

###Почтовые ящики - просмотр
Функция: **email**

Результат: список элементов
- **name** - Имя.
- **pop3** - Логин POP3.
- **disabled** - Почтовый ящик временно отключен.
- **vacation** - Автоответчик (vacation) активен..
- **forward** - Установлена пересылка почты..
- **antispam_disabled** - Антиспам отключен.
- **greylist_disabled** - Greylisting отключен.
- **note** - Примечание:.
- **size** - Размер. Атрибуты :
  - **used** - Использованное количество.
  - **limit** - Максимально возможное значение. 

###Почтовые ящики - создание, изменение
Функция: **email.edit**

Данная функция одновременно используется для просмотра параметров объекта, изменения объекта и создания нового объекта.

#####Просмотр параметров объекта:
- Параметры:
  - **elid** - уникальный идентификатор (элемент "name" из функции "email")
- Результат: список параметров объекта

#####Создание объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

#####Изменение объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - **elid** - уникальный идентификатор (элемент "name" из функции "email")
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

Список параметров объекта или дополнительных параметров запроса (см.выше):

- **name** - Имя.
- **domain** - Домен.
- **aliases** - Псевдонимы. (Одно или несколько значений, разделенных пробелом)
- **passwd** - Пароль.
- **confirm** - Подтверждение.
- **quota** - Макс. размер.
- **forward** - Слать копии писем на e-mail. (Одно или несколько значений, разделенных пробелом)
- **rmlocal** - Не сохранять в ящик. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".)
- **greylist** - Включить greylisting. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **greylist**.
- **spamassassin** - Включить SpamAssassin. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **sa**.
- **mailrate** - Количество отправляемых писем. (Числовое значение. Для указания "бесконечности" используйте "100000000".) Параметр зависим от возможности **mailrate**.
- **spamass_u_l** - Пользовательский SpamAssassin. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **usersa**. Активный параметр разрешает следующие параметры: 'required_score','rewrite_subject','report_safe','spam_action'
- **required_score** - Требуемая оценка. Параметр зависим от возможности **usersa**.
- **rewrite_subject** - Дописывать в поле "Тема". Параметр зависим от возможности **usersa**.
- **report_safe** - Тип отчета. Параметр зависим от возможности usersa.
- **spam_action** - Действие. Параметр зависим от возможности **usersa**.
- **note** - .

###WWW домены - просмотр
Функция: **wwwdomain**

Результат: список элементов
- **name** - Имя.
- **ip** - IP-адрес.
- **docroot** - Директория.
- **disabled** - WWW домен отключен.
- **cgi** - Данный WWW домен может использовать CGI.
- **wsgi** - Данный WWW домен может использовать WSGI.
- **php** - Данный WWW домен может использовать PHP.
- **ssi** - Данный WWW домен может использовать SSI.
- **frp** - Данный WWW домен может использовать расширение FrontPage.
- **ror** - Данный WWW домен может использовать Ruby on rails.
- **ssl** - Для доступа к данному WWW домену может быть использован протокол HTTPS.

###WWW домены - создание, изменение
Функция: **wwwdomain.edit**

Данная функция одновременно используется для просмотра параметров объекта, изменения объекта и создания нового объекта.

#####Просмотр параметров объекта:
- Параметры:
  - **elid** - уникальный идентификатор (элемент "name" из функции "wwwdomain")
- Результат: список параметров объекта

#####Создание объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

#####Изменение объекта:
- Параметры:
  - **sok** - значение параметра должно быть не пустым, обычно "yes".
  - **elid** - уникальный идентификатор (элемент "name" из функции "wwwdomain")
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

Список параметров объекта или дополнительных параметров запроса (см.выше):

- **domain** - Доменное имя.
- **alias** - Псевдонимы. (Одно или несколько значений, разделенных пробелом)
- **docroot** - Корневая папка.
- **owner** - Владелец.
- **ip** - IP-адрес.
- **ip6** - IPv6-адрес. Параметр зависим от возможности **ipv6**.
- **pool** - Пул приложений. Параметр зависим от возможности **iis**.
- **admin** - E-Mail администратора. Параметр зависим от возможности **webemail**.
- **charset** - Кодировка.
- **index** - Индексная страница. (Одно или несколько значений, разделенных пробелом)
- **autosubdomain** - Авто поддомены. Параметр зависим от возможности **asd**. Возможные значения:
  - **asdnone** - Отключены
  - **asddir** - В отдельной директории
  - **asdsubdir** - В поддиректории WWW домена.
- **php** - PHP. Возможные значения :
  - **phpnone** - Нет поддержки PHP
  - **phpmod** - PHP как модуль Apache
  - **phpcgi** - PHP как CGI
  - **phpfcgi** - PHP как FastCGI 
- **cgi** - Cgi-bin. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **cgi**.     Активный параметр разрешает следующие параметры: 'ror'
- **wsgi** - wsgi-scripts. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **wsgi**.
- **ssi** - SSI. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **ssi**.     Активный параметр разрешает следующие параметры: 'ssiext'
- **ssiext** - Расширения файлов SSI. Параметр зависим от возможности **ssi**.
- **frp** - FrontPage. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **frp**.     Активный параметр разрешает следующие параметры: 'fppasswd'
- **fppasswd** - Пароль для FrontPage. Параметр зависим от возможности **frp**.
- **ror** - Ruby on rails. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **ror**.     Активный параметр запрещает следующие параметры: 'autosubdomain'
- **ssl** - SSL. (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".) Параметр зависим от возможности **ssl**.     Активный параметр разрешает следующие параметры: 'sslport','cert'
- **sslport** - SSL порт. Параметр зависим от возможности ssl.
- cert - SSL сертификат. Параметр зависим от возможности **ssl**.
- **page_php_th** - .
- **disable_open_basedir** - . (Необязательный параметр. Чтобы включить данную опцию используйте значение "on".)
- **static_ext** - Расширения файлов. (Одно или несколько значений, разделенных пробелом)
- **static_regex** - Расширения файлов. (Одно или несколько значений, разделенных пробелом)

###WWW домены - просмотр, изменение для (Apache, Nginx)
Функция: **wwwdomain.plain**

Данная функция одновременно используется для просмотра и изменения параметров объекта

#####Просмотр параметров объекта:
- Параметры:
  - **elid** - уникальный идентификатор (элемент "name" из функции "wwwdomain")
- Результат: список параметров

#####Изменение объекта:
- Параметры:
  - **sok**- значение параметра должно быть не пустым, обычно "yes".
  - **elid** - уникальный идентификатор (элемент "name" из функции "wwwdomain")
  - дополнительные параметры запроса ...
- Результат: успешное выполнение операции или сообщение об ошибке

Список параметров объекта или дополнительных параметров запроса (см.выше):

- **adata** - Настройки Apache.
- **ndata** - Настройки Nginx.

###WWW домены - удаление
Функция: wwwdomain.delete

Параметры:

- **elid** - один или несколько уникальных идентификаторов объекта, разделенных запятой и следующим за ней пробелом ", ". Уникальный идентификатор - это элемент "name" из функции "wwwdomain".

Результат: успешное выполнение операции или сообщение об ошибке
