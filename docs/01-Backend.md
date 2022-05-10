# [Book] [Juha Hinkula] Full Stack Development with Spring Boot and React: Build modern and scalable full stack applications using the power of Spring Boot and React, 3rd Edition [ENG, 2022]

<br/>

# Part 1: Backend Programming with Spring Boot

<br/>

## 03. Using JPA to Create and Access a Database

<br/>

```
$ cd apps/backend
```

<br/>

```
$ chmod +x ./mvnw
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

<br/>

## 04. Creating a RESTful Web Service with Spring Boot

<br/>

```
$ chmod +x ./mvnw
$ ./mvnw spring-boot:run
```

<br/>

```
// GET
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/ \
    | jq
```

<br/>

**response:**

```
{
  "_links": {
    "cars": {
      "href": "http://localhost:8080/api/cars"
    },
    "owners": {
      "href": "http://localhost:8080/api/owners"
    },
    "profile": {
      "href": "http://localhost:8080/api/profile"
    }
  }
}
```

<br/>

```
// GET ALL CARS
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/cars \
    | jq
```

<br/>

**response:**

```
// GET ALL CARS
{
  "_embedded": {
    "cars": [
      {
        "brand": "Ford",
        "model": "Mustang",
        "color": "Red",
        "registerNumber": "ADF-1121",
        "year": 2021,
        "price": 59000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/3/owner"
          }
        }
      },
      {
        "brand": "Nissan",
        "model": "Leaf",
        "color": "White",
        "registerNumber": "SSJ-3002",
        "year": 2019,
        "price": 29000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/4"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/4"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/4/owner"
          }
        }
      },
      {
        "brand": "Toyota",
        "model": "Prius",
        "color": "Silver",
        "registerNumber": "KKO-0212",
        "year": 2020,
        "price": 39000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/5"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/5"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/5/owner"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/cars"
    },
    "profile": {
      "href": "http://localhost:8080/api/profile/cars"
    },
    "search": {
      "href": "http://localhost:8080/api/cars/search"
    }
  }
}

```


<br/>

```
// GET SINGLE CAR BY ID
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/cars/3 \
    | jq
```

<br/>

**response:**

```
{
  "brand": "Ford",
  "model": "Mustang",
  "color": "Red",
  "registerNumber": "ADF-1121",
  "year": 2021,
  "price": 59000,
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/cars/3"
    },
    "car": {
      "href": "http://localhost:8080/api/cars/3"
    },
    "owner": {
      "href": "http://localhost:8080/api/cars/3/owner"
    }
  }
}
```

<br/>

```
// GET ALL OWNERS
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/owners \
    | jq
```

<br/>

**response:**

```
{
  "_embedded": {
    "owners": [
      {
        "firstname": "John",
        "lastname": "Johnson",
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/owners/1"
          },
          "owner": {
            "href": "http://localhost:8080/api/owners/1"
          },
          "cars": {
            "href": "http://localhost:8080/api/owners/1/cars"
          }
        }
      },
      {
        "firstname": "Mary",
        "lastname": "Robinson",
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/owners/2"
          },
          "owner": {
            "href": "http://localhost:8080/api/owners/2"
          },
          "cars": {
            "href": "http://localhost:8080/api/owners/2/cars"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/owners"
    },
    "profile": {
      "href": "http://localhost:8080/api/profile/owners"
    }
  }
}
```

<br/>

```
// GET SINGE OWNER BY ID
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/owners/2 \
    | jq
```

<br/>

**response:**

```
{
  "firstname": "Mary",
  "lastname": "Robinson",
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/owners/2"
    },
    "owner": {
      "href": "http://localhost:8080/api/owners/2"
    },
    "cars": {
      "href": "http://localhost:8080/api/owners/2/cars"
    }
  }
}
```


<br/>

```
// GET CAR OWNER BY CAR ID
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/cars/5/owner \
    | jq
```

<br/>

```
{
  "firstname": "Mary",
  "lastname": "Robinson",
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/owners/2"
    },
    "owner": {
      "href": "http://localhost:8080/api/owners/2"
    },
    "cars": {
      "href": "http://localhost:8080/api/owners/2/cars"
    }
  }
}
```

<br/>

```
// GET CAR CARS BY CAR OWNER
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/owners/2/cars \
    | jq
```

<br/>

```
{
  "_embedded": {
    "cars": [
      {
        "brand": "Nissan",
        "model": "Leaf",
        "color": "White",
        "registerNumber": "SSJ-3002",
        "year": 2019,
        "price": 29000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/4"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/4"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/4/owner"
          }
        }
      },
      {
        "brand": "Toyota",
        "model": "Prius",
        "color": "Silver",
        "registerNumber": "KKO-0212",
        "year": 2020,
        "price": 39000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/5"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/5"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/5/owner"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/owners/2/cars"
    }
  }
}
```

<br/>

```
// SEARCH BY BRAND
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/cars/search/findByBrand?brand=Ford \
    | jq
```


<br/>

**response:**

```
{
  "_embedded": {
    "cars": [
      {
        "brand": "Ford",
        "model": "Mustang",
        "color": "Red",
        "registerNumber": "ADF-1121",
        "year": 2021,
        "price": 59000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/3/owner"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/cars/search/findByBrand?brand=Ford"
    }
  }
}

```

<br/>

```
// SEARCH BY COLOR
$ curl \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/api/cars/search/findByColor?color=Red \
    | jq
```

<br/>

**response:**

```
{
  "_embedded": {
    "cars": [
      {
        "brand": "Ford",
        "model": "Mustang",
        "color": "Red",
        "registerNumber": "ADF-1121",
        "year": 2021,
        "price": 59000,
        "_links": {
          "self": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "car": {
            "href": "http://localhost:8080/api/cars/3"
          },
          "owner": {
            "href": "http://localhost:8080/api/cars/3/owner"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:8080/api/cars/search/findByColor?color=Red"
    }
  }
}
```


<br/>

## 05. Securing and Testing Your Backend


<br/>

```
// Username: user, password: user
// Username: admin, password: admin
```

<br/>

```
// RUN TESTS
$ mvn clean install
```

<br/>

```
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] 
```

<br/>

```
$ chmod +x ./mvnw
$ ./mvnw spring-boot:run
```

<br/>

```
mysql> SELECT * FROM user;
+----+--------------------------------------------------------------+-------+----------+
| id | password                                                     | role  | username |
+----+--------------------------------------------------------------+-------+----------+
|  1 | $2a$10$NVM0n8ElaRgg7zWO1CxUdei7vWoPg91Lz2aYavh9.f9q0e4bRadue | USER  | user     |
|  2 | $2a$10$8cjz47bjbR4Mn8GMg9IZx.vyjhLXR/SKKMSZ9.mP9vpMu0ssKi8GW | ADMIN | admin    |
+----+--------------------------------------------------------------+-------+----------+
2 rows in set (0.00 sec)
```

<br/>

```
// LOGIN
$ curl -v  \
     --data '{
       "username":"user",
       "password":"user"
       }' \
     --header "Content-Type: application/json" \
     --request POST http://localhost:8080/login
```

<br/>

**response:**

```
*   Trying 127.0.0.1:8080...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> POST /login HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.68.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 61
> 
* upload completely sent off: 61 out of 61 bytes
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 
< Vary: Origin
< Vary: Access-Control-Request-Method
< Vary: Access-Control-Request-Headers
< Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1c2VyIiwiZXhwIjoxNjUyMjg4NTYwfQ.JxDopiXCTkWZpbhL_fEFSWTc1Coj_gf_9kCIhV0x4TQ
< Access-Control-Expose-Headers: Authorization
< X-Content-Type-Options: nosniff
< X-XSS-Protection: 1; mode=block
< Cache-Control: no-cache, no-store, max-age=0, must-revalidate
< Pragma: no-cache
< Expires: 0
< X-Frame-Options: DENY
< Content-Length: 0
< Date: Tue, 10 May 2022 17:02:40 GMT
```

<br/>

```
$ AUTH_TOKEN=eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1c2VyIiwiZXhwIjoxNjUyMjg4NTYwfQ.JxDopiXCTkWZpbhL_fEFSWTc1Coj_gf_9kCIhV0x4TQ
```

<br/>

```
// GET CARS
// SEARCH BY COLOR
// OK!
$ curl \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request GET \
    --url http://localhost:8080/api/cars/search/findByColor?color=Red \
    | jq
```


<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://javadev.org/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://javadev.ru/chat/">Телеграм чат</a>