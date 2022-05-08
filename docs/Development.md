# [Book] [Juha Hinkula] Full Stack Development with Spring Boot and React: Build modern and scalable full stack applications using the power of Spring Boot and React, 3rd Edition [ENG, 2022]

<br/>

### 03. Using JPA to Create and Access a Database

```
$ cd apps/backend
```

<br/>

```
$ ./mvnw spring-boot:run
```

<br/>

```
$ mysql --user=root --password=pA55w0rd123 -h 127.0.0.1 db
```

<br/>

```
mysql> SELECT DATABASE();
```

<br/>

```
mysql> use db;
```

<br/>

```
mysql> SELECT * FROM owner;
+---------+-----------+----------+
| ownerid | firstname | lastname |
+---------+-----------+----------+
|       1 | John      | Johnson  |
|       2 | Mary      | Robinson |
+---------+-----------+----------+
2 rows in set (0.00 sec)

```

<br/>

```
mysql> SELECT * FROM car;
+----+--------+--------+---------+-------+-----------------+------+-------+
| id | brand  | color  | model   | price | register_number | year | owner |
+----+--------+--------+---------+-------+-----------------+------+-------+
|  3 | Ford   | Red    | Mustang | 59000 | ADF-1121        | 2021 |     1 |
|  4 | Nissan | White  | Leaf    | 29000 | SSJ-3002        | 2019 |     2 |
|  5 | Toyota | Silver | Prius   | 39000 | KKO-0212        | 2020 |     2 |
+----+--------+--------+---------+-------+-----------------+------+-------+
3 rows in set (0.00 sec)
```

<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://javadev.org/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://javadev.ru/chat/">Телеграм чат</a>