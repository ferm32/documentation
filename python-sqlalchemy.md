### SQLAlchemy ORM

Здесь представлен и полностью описан Объектный Реляционный Сопоставитель (Object Relational Mapper, ORM). Если Вы хотите работать с более высокоуровневым SQL (который в случае использования ORM формируется автоматически, также как автоматизированно сохраняются объекты Python), начните с Руководсва.

#### Проверка версии
Можно быстро проверить, используем ли мы последнюю версию SQLAlchemy (на апрель 2013 года это 0.8.0):

    >>> import sqlalchemy
    >>> sqlalchemy.__version__ 
    0.8.0
  
#### Соединение с БД
В данном руководстве мы будем испоьлзовать базу данных SQLite, размещённую полностью в оперативной памяти. Для соединения с ней мы используем `create_engine()`:

    >>> from sqlalchemy import create_engine
    >>> engine = create_engine('sqlite:///:memory:', echo=True)

Флаг `echo` это включение журнала регистрации действий SQLAlchemy, который работает через стандартный модуль Python `logging`. Когда он включен, мы увидим все сгенерированные команды SQL. Если Вы, работая с данным Руководством, хотите генерировать не так много выходной информации, присвойте этому параметру `False`.

 This tutorial will format the SQL behind a popup window so it doesn’t get in our way; just click the “SQL” links to see what’s being generated.

The return value of create_engine() is an instance of Engine, and it represents the core interface to the database, adapted through a dialect that handles the details of the database and DBAPI in use. In this case the SQLite dialect will interpret instructions to the Python built-in sqlite3 module.

The Engine has not actually tried to connect to the database yet; that happens only the first time it is asked to perform a task against the database. We can illustrate this by asking it to perform a simple SELECT statement:

sql>>> engine.execute("select 1").scalar()
1

As the Engine.execute() method is called, the Engine establishes a connection to the SQLite database, which is then used to emit the SQL. The connection is then returned to an internal connection pool where it will be reused on subsequent statement executions. While we illustrate direct usage of the Engine here, this isn’t typically necessary when using the ORM, where the Engine, once created, is used behind the scenes by the ORM as we’ll see shortly.