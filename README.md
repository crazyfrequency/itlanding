# Кратко
```
В случие перехода на несуществующую страницу отправляется заранее заготовленная страница позволяющая перейти на главную
В случие использования http аналогично(просим перейти на https)
главная "/"
отправка "/request" или другое(на усмотрение front-end разработчика)
Всё остальное также на усмотрение front-end разработчика
```
про логин и пароль:
`не должны содержать пробелы и странные символы`


# API
### добавление запроса от потенциального заказчика
##### `PUT` "/api/request"
Json параметры:
| поле | тип | описание | обязательное | по умолчанию |
|:----:|:---:|:--------:|:------------:|:------------:|
|user|string| фио | да | - |
|title|string|заголовок|нет|id|
|description|string|краткое описание|да| - |
|email|string|контакты|да| - |

Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | "ok" | успешно |
| 400 |"Bad Request"|плохой запрос|
| 418 |"I'm a teapot"|сервер отказывается варить кофе в чайнике|
| 500 | "Internal Server Error" | ошибка сервера |
___
### просмотр запроса по id
##### `GET` "/api/request/`{id}`"
```без тела запроса```</br>
Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | JSON | Успешно |
| 400 |"Bad Request"|плохой запрос|
| 401 |"Unauthorized"|не авторизован|
| 500 | "Internal Server Error" | ошибка сервера |

JSON результат:
| поле | тип | описание |
|:----:|:---:|:--------:|
|id|integer| id запроса |
|user|string| фио |
|title|string|заголовок|
|description|string|краткое описание|
|email|string|контакты|
|date |date(unix)|дата получения| 
___
### обновление статуса запроса (отвеченное или новое)
##### `POST` "/api/request/`{id}`" 
Json параметры:
| поле | тип | описание | обязательное | по умолчанию |
|:----:|:---:|:--------:|:------------:|:------------:|
| status | integer | request status | да | 1 |

Request status:
| значение | описание |
|:--------:|:--------:|
| 0 | не прочитанно |
| 1 | прочитано |
Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | JSON | Успешно |
| 400 |"Bad Request"|плохой запрос|
| 401 |"Unauthorized"|не авторизован|
| 500 | "Internal Server Error" | ошибка сервера |

___
### получение списка запросов
##### `GET` "/api/requests" 

```без тела запроса```</br>
Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | JSON | Успешно |
| 400 |"Bad Request"|плохой запрос|
| 401 |"Unauthorized"|не авторизован|
| 500 | "Internal Server Error" | ошибка сервера |

JSON результат:
| поле | тип | описание |
|:----:|:---:|:--------:|
|requests| request[] | массив request объектов |

request:
| поле | тип | описание |
|:----:|:---:|:--------:|
|id|integer| id запроса |
|user|string| фио |
|title|string|заголовок|
|date |date(unix)|дата получения| 
___
### логин
##### `POST` "/api/login" 
Json параметры:
| поле | тип | описание | обязательное | по умолчанию |
|:----:|:---:|:--------:|:------------:|:------------:|
| username | string(16) | имя пользователя | да | - |
| password | string(256) | ипароль | да | - |

Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | "ok" | авторизован |
| 400 |"Bad Request"|не верный логин или пароль|
| 418 |"I'm a teapot"|сервер отказывается варить кофе в чайнике|
| 500 | "Internal Server Error" | ошибка сервера |
___
### проверка логина
##### `GET` "/api/login" 
```без тела запроса```</br>
Коды результата:
| код | body ответ | описание |
|:---:|:----------:|:--------:|
| 200 | "ok" | авторизован |
| 401 |"Unauthorized"|не авторизован|
| 418 |"I'm a teapot"|сервер отказывается варить кофе в чайнике|
| 500 | "Internal Server Error" | ошибка сервера |
