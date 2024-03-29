
# MySQL и PostgreSQL / настройка MongoDB

## 1. Введение

Данное руководство построено на примере
[Tech Differences](https://techdifferences.com/difference-between-mysql-and-postgresql.html "Tech Differences"), [Node Postgres ](https://node-postgres.com/ "Node Postgres ") и [Get started postgresqltutorial](http://www.postgresqltutorial.com/postgresql-select/ "Get started postgresqltutorial")
 

## 2. Обзор
### Разница между MySQL и PostgreSQL 

#### Definition of MySQL

Определение MySQL MySQL - это система управления реляционными базами данных с открытым исходным кодом. 

Имя MySQL - это сочетание имени дочери соучредителя Майкла Видениуса «My» и SQL - аббревиатуры для языка структурированных запросов.

MySQL является продуктом корпорации Oracle. MySQL поддерживает много стандарта SQL. 

Что касается операционной системы, то MySQL поддерживается практически всеми операционными системами, такими как Windows, Mac OS X, Linux, BSD, UNIX, z / OS, Symbian, AmigaOS.

Система баз данных MySQL используется в сети для добавления, доступа и управления данными в Интернете.

В MySQL инструмент phpMyAdmin отвечает за предоставление графического интерфейса и интерфейса SQL. 

MySQL не предлагает опцию резервного копирования, но использует Mysqldump и инструмент XtraBackup для резервного копирования. 

MySQL предлагает временные таблицы, но не обеспечивает материализованное представление. Поскольку MySQL является только управлением реляционной базой данных, он не предоставляет объект предметной области.



#### Definition of PostgreSQL

PostgreSQL - это система управления объектно-реляционными базами данных с открытым исходным кодом. 

Группа глобального развития разрабатывает PostgreSQL. Он использует множество стандартов SQL. 

PostgreSQL полностью совместим с ACID. Поддержка внешнего ключа, триггеры и объединение доступны в PostgreSQL. 

PostgreSQL поддерживается операционными системами Windows, Mac OS X, Linux и BSD, но не операционными системами UNIX, z / OS, Symbian, AmigaOS. 

Язык программирования PostgreSQL очень расширяем. 

PostgreSQL использует инструмент pgAdmin для обеспечения графического интерфейса и интерфейса SQL. 

PostgresSQL предлагает возможность онлайн резервного копирования. Он предоставляет временные таблицы, а также материализованное представление. и это также обеспечивает объект предметной области.

## 3. Создание и подключение базы данных
### PostgreSQL Tutorial 

Более подробно можно почитать здесь https://postgrespro.ru/docs/

PSQL Shell (psql)
1. Введите информацию об учетной записи для входа на сервер базы данных PostgreSQL. Вы можете использовать значение по умолчанию, предоставляемое psql, нажав клавишу Enter.
```sql
       Server [localhost]:
       Database [postgres]:
       Port [5432]:
       Username [postgres]:
       Password for user postgres:
```

2. Введите следующую инструкцию CREATE DATABASE, чтобы создать новую базу данных admindb.
```sql
       CREATE DATABASE admindb;
```

Выделите отдельные строки с помощью оператора [DISTINCT](http://www.postgresqltutorial.com/postgresql-select-distinct/ "DISTINCT")

Сортировать строки с помощью предложения [ORDER BY](http://www.postgresqltutorial.com/postgresql-order-by/ "ORDER BY")
 
Фильтрация строк с использованием предложения [WHERE](http://www.postgresqltutorial.com/postgresql-where/ "WHERE")

Выберите подмножество строк в таблице, используя предложение [LIMIT](http://www.postgresqltutorial.com/postgresql-limit/ "LIMIT") и [FETCH](http://www.postgresqltutorial.com/postgresql-fetch/ "FETCH")


 Группируйте строки в группы с помощью предложения [GROUP BY](http://www.postgresqltutorial.com/postgresql-order-by/ "GROUP BY")
 
 Фильтруйте группы с помощью предложения [HAVING](http://www.postgresqltutorial.com/postgresql-having/"HAVING")
  
 Объединяйте с другими таблицами, используя соединения, такие как [JOINS](http://www.postgresqltutorial.com/postgresql-joins/ "JOINS")  

Выполните операции установки, используя [UNION](http://www.postgresqltutorial.com/postgresql-union/ "UNION"), [INTERSECT](http://www.postgresqltutorial.com/postgresql-intersect/ "INTERSECT") и [EXCEPT](http://www.postgresqltutorial.com/postgresql-tutorial/postgresql-except/  "EXCEPT")



     \l                          - список баз данных
     \dt                         - список всех таблиц
     \d table                    - структура таблицы table
     \c databaseName             - подключиться к databaseName
     
узнать текущий путь: 
```sql
SHOW data_directory;       
```
cписок пользователей
```sql
SELECT * FROM pg_shadow;    
```
cписок баз данных
```sql
SELECT * FROM pg_database;  
```   
переименовать template1 в todo
```sql
ALTER DATABASE template1 RENAME TO todo      -
```   
   
В качестве проверки подключения базы данных к node-server можно использовать следущую запись
   ```js
      var pgp = require("pg-promise")(/*options*/);
      var db = pgp("postgres://ilinoa:1234@localhost:5432/postgres");
                 // postgres://username:password@host:port/database
      db.one("SELECT $1 AS value", 123)
      .then(function (data) {
        console.log("DATA:", data.value);
      })
      .catch(function (error) {
        console.log("ERROR:", error);
      });
   ```
  
  Вывод программы DATA: 123

## Начало работы

 1. Создадим базу данных и добавим данные
```sql
    CREATE TABLE users(
      name VARCHAR(20),
      age SMALLINT
    );
    
    
    INSERT INTO users values('Billy John', 23);
    INSERT INTO users values('Smith George', 23);
    INSERT INTO users values('Ernest Cook', 34);
    INSERT INTO users values('Marshall Ballard', 35);
    INSERT INTO users values('Joann Riley', 26);
    INSERT INTO users values('Pearl Pearson', 43);
 ```   

2. Необходимо убедиться в настроке package.json
```js
     {
       "name": "psql",
       "version": "1.0.0",
       "description": "",
       "main": "index.js",
       "scripts": {
         "test": "echo \"Error: no test specified\" && exit 1"
       },
       "author": "Oleg",
       "license": "ISC",
       "dependencies": {
         "express": "^4.17.1",
         "node": "^12.7.0",
         "pg": "^7.12.0",
         "server.js": "^1.0.0"
       }
     }
```
Создадим сервер на node-express и создадим запрос "SELECT * FROM users"

```js
    var express = require('express');
    var pg = require('pg');
    var app = express();

    var connectionString = 'postgres://ilinoa:1234@localhost:5430/todo';

    const client = new pg.Client(connectionString);
    
    //Проверим подлючение к базе данных 
    client.connect(function(error) {
     //callback
     if (!!error) { console.log('Error'+ error.message); }
     else {  console.log('Connected'); } 
    });

    app.get('/', function(require, response) {
     // about postgresql
     client.query("SELECT * FROM users", function(error, rows) {
      // callback
      if (!!error) {
       console.log('Error in the query');
      } else {
       // parse wiyh your rows/fields
       console.log('Successful query');
       console.log(rows.name);
       response.json(rows);
      }
      });
    });

    app.listen(3000);
 ```



 
## Обзор MongoDB


Запуск MongoDB
```db
mongo --host localhost:27017
```

Создать базу данных `mydatabase`
```db
use mydatabase
```

Как настроить Mongo читайте здесь - https://medium.com/founding-ithaka/setting-up-and-connecting-to-a-remote-mongodb-database-5df754a4da89
