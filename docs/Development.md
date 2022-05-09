# [Book] [Juha Hinkula] Full Stack Development with Spring Boot and React: Build modern and scalable full stack applications using the power of Spring Boot and React, 3rd Edition [ENG, 2022]

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



<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://javadev.org/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://javadev.ru/chat/">Телеграм чат</a>