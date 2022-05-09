1.2) скачал и установил

vagrant@vagrant:~$ mysql --version

mysql  Ver 14.14 Distrib 5.7.38, for Linux (x86_64) using  EditLine wrapper

заходим в mysql

sudo mysql -u root -p

3)для тестов выбрал схему библиотека --> жанры книг --> авторы

создал базу 

create database library;

выбираем базу
use library;


4) создаем таблицы 

create table prose(id int, name varchar(255), surname varchar(255));

выбрал варчар 255, поскольку до 255 он будет всеравно занимать 1 байт, но информационой ошибки при переполнии сомволов не будет

create table fantasy(id int, name varchar(255), surname varchar(255));

create table detective(id int, name varchar(255), surname varchar(255));

смотрим наличие таблиц
mysql> show tables;

+-------------------+

| Tables_in_library |

+-------------------+

| detective         |

| fantasy           |

| prose             |

+-------------------+

5) наполняю таблицы, указываю одну коменду наполнения со всех 

insert into detective(id, name, surname)values('1', 'Adams','Clifton');

смотрим содержимое таблицы

mysql> select * from detective;

+------+-----------+-----------+

| id   | name      | surname   |

+------+-----------+-----------+

| NULL | Adams     | Clifton   |

|    1 | Adams     | Clifton   |

|    2 | Eric      | Ambler    |

|    3 | Lin       | Anderson  |

|    4 | Patrick   | Anderson  |

|    6 | Baldacci  | David     |

|    7 | Linwood   | Barclay   |

|    8 | Raymond   | Benson    |

|    9 | Josh      | Bazel     |

|   10 | John      | Burdett   |

|    5 | Charlotte | Armstrong |

+------+-----------+-----------+

11 rows in set (0.00 sec)

mysql> insert into prose(id, name, surname)values('1', 'Trezza','Azopardi');

mysql> select * from prose;

+------+-----------+-----------------+

| id   | name      | surname         |

+------+-----------+-----------------+

|    1 | Trezza    | Azopardi        |

|    2 | Charlotte | Aisse           |

|    3 | Sadriddin | Aini            |

|    4 | Maigull   | Akselsson       |

|    5 | Mitsos    | Alexandropoulos |

|    6 | Jane      | Alpert          |

|    7 | Georges   | Amadou          |

|    8 | Niccolo   | Ammaniti        |

|    9 | Ivo       | Andric          |

|   10 | Gercho    | Atanasov        |

+------+-----------+-----------------+

10 rows in set (0.00 sec)



mysql> insert into fantasy(id, name, surname)values('1', 'Robert','Alter');

mysql> select * from fantasy;

+------+-----------+-----------+

| id   | name      | surname   |

+------+-----------+-----------+

|    1 | Robert    | Alter     |

|    2 | Pamela    | Adams     |

|    3 | Katherine | Azaro     |

|    4 | Isaac     | Asimov    |

|    5 | Larry     | Eisenberg |

|    6 | Ryunosuke | Akutagawa |

|    7 | Stevie    | Allen     |

|    8 | Stephen   | Baxter    |

|    9 | Arpad     | Balazs    |

|   10 | Stan      | Barstow   |

+------+-----------+-----------+

10 rows in set (0.00 sec)

6) делаем селект второй строки по имени
mysql> select @n:= name from prose where id = 2;

+-----------+

| @n:= name |

+-----------+

| Charlotte |

+-----------+

1 row in set (0.00 sec)

mysql> select * from prose;

+------+-----------+-----------------+

| id   | name      | surname         |

+------+-----------+-----------------+

|    1 | Trezza    | Azopardi        |

|    2 | Charlotte | Aisse           |

|    3 | Sadriddin | Aini            |

|    4 | Maigull   | Akselsson       |

|    5 | Mitsos    | Alexandropoulos |

|    6 | Jane      | Alpert          |

|    7 | Georges   | Amadou          |

|    8 | Niccolo   | Ammaniti        |

|    9 | Ivo       | Andric          |

|   10 | Gercho    | Atanasov        |

+------+-----------+-----------------+

10 rows in set (0.00 sec)


mysql> select surname from prose group by surname;

+-----------------+

| surname         |

+-----------------+

| Aini            |

| Aisse           |

| Akselsson       |


| Alexandropoulos |

| Alpert          |

| Amadou          |

| Ammaniti        |

| Andric          |

| Atanasov        |

| Azopardi        |

+-----------------+

10 rows in set (0.00 sec)

mysql> select surname from prose order by surname;

+-----------------+

| surname         |

+-----------------+

| Aini            |


| Aisse           |

| Akselsson       |

| Alexandropoulos |

| Alpert          |

| Amadou          |

| Ammaniti        |

| Andric          |

| Atanasov        |

| Azopardi        |

+-----------------+

10 rows in set (0.01 sec)



7)
alter table prose add book varchar(255);

mysql> select * from prose;

+------+-----------+-----------------+------+

| id   | name      | surname         | book |

+------+-----------+-----------------+------+

|    1 | Trezza    | Azopardi        | NULL |

|    2 | Charlotte | Aisse           | NULL |

|    3 | Sadriddin | Aini            | NULL |

|    4 | Maigull   | Akselsson       | NULL |

|    5 | Mitsos    | Alexandropoulos | NULL |

|    6 | Jane      | Alpert          | NULL |

|    7 | Georges   | Amadou          | NULL |

|    8 | Niccolo   | Ammaniti        | NULL |

|    9 | Ivo       | Andric          | NULL |

|   10 | Gercho    | Atanasov        | NULL |

+------+-----------+-----------------+------+

10 rows in set (0.01 sec)

mysql> rename table prose to prose2;

mysql> show tables;
+-------------------+
| Tables_in_library |
+-------------------+
| detective         |
| fantasy           |
| prose2            |
+-------------------+
3 rows in set (0.00 sec)

название таблицы вернул обратно

mysql> truncate table prose;

mysql> select * from prose;

Empty set (0.00 sec)

insert into prose(id, name, surname, book)values('1','Trezza','Azopardi','Ukrytie');

mysql> select * from prose;

+------+--------+----------+---------+

| id   | name   | surname  | book    |

+------+--------+----------+---------+

|    1 | Trezza | Azopardi | Ukrytie |

+------+--------+----------+---------+

alter table prose add library varchar(255);

mysql> mysql> select * from prose;

+------+--------+----------+---------+---------+

| id   | name   | surname  | book    | library |

+------+--------+----------+---------+---------+

|    1 | Trezza | Azopardi | Ukrytie | NULL    |

+------+--------+----------+---------+---------+

mysql> update prose set library='National Library of Ukraine';

mysql> select * from prose;

+------+--------+----------+---------+-----------------------------+

| id   | name   | surname  | book    | library                     |

+------+--------+----------+---------+-----------------------------+

|    1 | Trezza | Azopardi | Ukrytie | National Library of Ukraine |

+------+--------+----------+---------+-----------------------------+


delete from prose where library='National Library of Ukraine';

mysql> select * from prose;

Empty set (0.00 sec)

mysql> merge detective as target using fantasy as source on source.id = target.id when not matched by target then insert (id,name, surname) 

values (source.id,source.name, source.surname);
8) вобщем команда грант может навешивать пермишины и создавать юзеров в крации мы говорим чтобы грант дал пермишин селект на базу с табличкой 

для пользователя с паролем 1

grant select on library.detective to kent@local.host identified by '1';

чтобы не бегать туда сюда, можно посмотреть гранты для пользлвателя

mysql> show grants for kent@local.host;

+--------------------------------------------------------------+

| Grants for kent@local.host                                   |

+--------------------------------------------------------------+

| GRANT USAGE ON *.* TO 'kent'@'local.host'                    |

| GRANT SELECT ON `library`.`detective` TO 'kent'@'local.host' |

+--------------------------------------------------------------+

2 rows in set (0.00 sec)

забирает права для пользователя которого мы недавно создали

mysql> revoke select on library.detective from kent@local.host;

mysql> show grants for kent@local.host;

+-------------------------------------------+

| Grants for kent@local.host                |

+-------------------------------------------+

| GRANT USAGE ON *.* TO 'kent'@'local.host' |

+-------------------------------------------+

1 row in set (0.00 sec)

даем право пользователю раздавать права

mysql> grant grant option on library.detective to den@local.host identified by '1';

mysql> show grants for den@local.host;

+------------------------------------------------------------------------------+

| Grants for den@local.host                                                    |

+------------------------------------------------------------------------------+

| GRANT USAGE ON *.* TO 'den'@'local.host'                                     |

| GRANT USAGE ON `library`.`detective` TO 'den'@'local.host' WITH GRANT OPTION |

+------------------------------------------------------------------------------+

2 rows in set (0.00 sec)

лучше выпилнять такую команду для моминтального начисления грантов

mysql> flush privileges;

9)

mysql> select user,host,authentication_string from mysql.user;

+------------------+------------+-------------------------------------------+

| user             | host       | authentication_string                     |

+------------------+------------+-------------------------------------------+

| root             | localhost  |                                           |

| mysql.session    | localhost  | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE |

| mysql.sys        | localhost  | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE |

| debian-sys-maint | localhost  | *2DB0A19D51ADB2DC935CE27FEA5648849F34A8D0 |

| kent             | local.host | *E6CC90B878B948C35E92B003C792C46C58C4AF40 |

| den              | local.host | *E6CC90B878B948C35E92B003C792C46C58C4AF40 |
+------------------+------------+-------------------------------------------+

6 rows in set (0.00 sec)



10) есть много способов создать бэкап

sudo cp -r /var/lib/mysql/library /home/vagrant/

sudo mysqldump -uroot -p --all-databases > all-databases.sql

11) mysql> drop table prose;

12) sudo mysql -uroot -p mysql < all-databases.sql

mysql> show tables;

+-------------------+

| Tables_in_library |

+-------------------+

| detective         |

| fantasy           |

| prose             |

+-------------------+

3 rows in set (0.00 sec)


13)

sudo mysqldump -u root -p library > buckup.sql

sudo mysql -u admin -p -h library.ca75lcciknob.eu-central-1.rds.amazonaws.com -D library < buckup.sql

14)

mysql -u admin -p -h library.ca75lcciknob.eu-central-1.rds.amazonaws.com --port 3306

по innodb можно понять что это RDS

mysql> show databases;

+--------------------+

| Database           |

+--------------------+

| information_schema |

| innodb             |

| library            |

| mysql              |

| performance_schema |

| sys                |

+--------------------+

6 rows in set (0.04 sec)


15)

mysql> select surname from detective order by surname;

+-----------+

| surname   |

+-----------+

| Ambler    |

| Anderson  |

| Anderson  |

| Armstrong |

| Barclay   |

| Bazel     |

| Benson    |

| Burdett   |

| Clifton   |

| Clifton   |

| David     |

+-----------+

11 rows in set (0.04 sec)

mysql> select * from detective;

+------+-----------+-----------+

| id   | name      | surname   |

+------+-----------+-----------+

| NULL | Adams     | Clifton   |

|    1 | Adams     | Clifton   |

|    2 | Eric      | Ambler    |

|    3 | Lin       | Anderson  |

|    4 | Patrick   | Anderson  |

|    6 | Baldacci  | David     |

|    7 | Linwood   | Barclay   |

|    8 | Raymond   | Benson    |

|    9 | Josh      | Bazel     |

|   10 | John      | Burdett   |

|    5 | Charlotte | Armstrong |

+------+-----------+-----------+

11 rows in set (0.03 sec)

mysql> select surname from detective group by surname;

+-----------+

| surname   |

+-----------+

| Ambler    |

| Anderson  |

| Armstrong |

| Barclay   |

| Bazel     |

| Benson    |

| Burdett   |

| Clifton   |

| David     |

+-----------+

9 rows in set (0.04 sec)


16) дамп можно сделат так

sudo mysqldump -uroot --result-file=all.sql --all-databases

17) решил развернуть в докере

docker run --name mongo_epam -e MONGODB_DATABASE=admin -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=6196300 -p 27019:27017 

--rm -d mongo

docker exec -it 9b5f3338a3c2 /bin/bash

mongo -u root -p 6196300 --authenticationDatabase admin


> show dbs;

admin   0.000GB

config  0.000GB

local   0.000GB


18) можно создавать колекцию так

use library

19)

> db.memberships.insertOne({title: 'Basic 6 month', duration: 6, price: {value: 1000, currency: 'UAH'}})

{
	"acknowledged" : true,

	"insertedId" : ObjectId("6278f836064cfbf458098a86")

}


20)

> db.memberships.find({}).pretty()

{

	"_id" : ObjectId("6278f836064cfbf458098a86"),

	"title" : "Basic 6 month",

	"duration" : 6,

	"price" : {

		"value" : 1000,

		"currency" : "UAH"
	}

}
