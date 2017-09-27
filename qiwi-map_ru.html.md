---
title: QIWI-Terminal-Map API 1.0.0

search: true

metatitle: QIWI-Terminal-Map API 1.0.0

metadescription: API Карты терминалов QIWI позволяет установить местонахождение терминалов QIWI на территории РФ.

language_tabs:
  - shell

services:



toc_footers:
  - <a href='/'>На главную</a>
  - <a href='mailto:api_help@qiwi.com'>Обратная связь</a>

---

# API Карты терминалов QIWI {#qiwi-map}

###### Последнее обновление: 2017-08-02 | [Редактировать на GitHub](https://github.com/QIWI-API/qiwi-map-docs/blob/master/qiwi-map_ru.html.md)

API Карты терминалов QIWI позволяет установить местонахождение терминалов QIWI на территории РФ.

<aside class="notice">
С открытым исходным кодом приложения карты терминалов можно ознакомиться <a href="https://github.com/QIWI-API/qiwi-map">по ссылке</a>
</aside>

<img src="/images/qiwi-map.png" />

## Поиск по адресу {#adress-search}

Запрос выполняет поиск терминалов по заданному адресу и ряду дополнительных параметров.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/locator/address?address=%D0%90%D0%BD%D0%B4%D1%80%D0%BE%D0%BF%D0%BE%D0%B2%D0%B0%20&page=1&ttpId=4'

HTTP/1.1 200 OK
Content-Type: text/json

{
  "page":1,
  "pageCount":2,
  "pageSize":1000,
  "terminals": [
    {
      "terminalId":8343266,
      "ttpId":4,
      "coordinate":
        {
          "latitude":51.533504,
          "longitude":46.016651,
          "precision":500
        },
      "verified":false,
      "lastActive":"2017-07-01T19:27:09.935",
      "address":"г Саратов, им Чапаева В.И. ул, 67"
    },
    {
      "terminalId":8569481,
      "ttpId":4,
      "coordinate": {
          "latitude":51.59005,
          "longitude":46.023022,
          "precision":101
      },
      "verified":false,
      "lastActive":"2017-09-20T12:11:41.427",
      "address":"г Саратов, Танкистов ул, 135"
    }
  ]
}

~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/locator/address</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: application/json;charset=UTF-8 - формат ответа JSON</li>
        </ul>
    </li>
</ul>


<ul class="nestedList params">
    <li><h3>Параметры</h3><span>Параметры передаются в строке запроса</span>
    </li>
</ul>

Параметр|Описание|Тип|Обяз.
---------|--------|---|------
address | URL-закодированные данные адреса терминала в произвольной форме (город, улица и т.д.) | String|+
page | Номер страницы в выгрузке | Long|+
ttpId | Отбор по типу терминала: `19` - терминалы партнеров; `4` - терминалы QIWI | Long |-
verified | Адрес терминала верифицирован и является актуальным | Boolean|-
activeWithinMinutes | Активность в течение X минут |Long|-



<h3 class="request">Ответ ←</h3>

~~~json
{
  "page":1,
  "pageCount":2,
  "pageSize":1000,
  "terminals": [
    {
      "terminalId":8343266,
      "ttpId":4,
      "coordinate": {
          "latitude":51.533504,
          "longitude":46.016651,
          "precision":500
      },
      "verified":false,
      "lastActive":"2017-07-01T19:27:09.935",
      "address":"г Саратов, им Чапаева В.И. ул, 67"
    },
    {
      "terminalId":8569481,
      "ttpId":4,
      "coordinate":
        {
          "latitude":51.59005,
          "longitude":46.023022,
          "precision":101
        },
      "verified":false,
      "lastActive":"2017-09-20T12:11:41.427",
      "address":"г Саратов, Танкистов ул, 135"
    }
  ]
}
~~~

Параметр|Описание|Тип
---------|--------|---
page | Номер страницы в выдаче результатов запроса. Количество терминалов одной страницы не может превышать 1000 | String
pageCount | Количество страниц в выдаче результатов запроса | Long
pageSize | Количество терминалов в одной странице. Максимальное - 1000| Long
terminals | Массив найденных терминалов | Array
adress | Адрес терминала | String
coordinate | Объект координат терминала |Object
coordinate.latitude | Широта |Double
coordinate.longtitude | Долгота |Double
coordinate.precision | Погрешность |Double
lastActive | Время последней активности терминала |Date
terminalId | Номер терминала |Long
ttpId | Тип терминала: `19` - терминал партнера; `4` - терминал QIWI |Number
verified | Адрес терминала верифицирован и является актуальным |Boolean

## Поиск по координатам {#area-search}

Поиск терминалов в окрестности заданных координат.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/locator/v2/nearest/cluster?latNW=57.05930421115318&lngNW=59.97245277050781&zoom=10'

HTTP/1.1 200 OK
Content-Type: text/json

[
  {
    "terminalId":10352688,
    "ttpId":4,
    "lastActive":"2017-09-20T12:10:34.288",
    "count":7,
    "coordinate": {
        "latitude":55.6869467142857,
        "longitude":37.385664,
        "precision":58
    },
    "address":"Одинцовский р-н, д Немчиново, ?, 76",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  },
  {
    "terminalId":10356000,
    "ttpId":4,
    "lastActive":"2017-09-20T12:10:47.679",
    "count":16,
    "coordinate": {
        "latitude":55.690496687499994,
        "longitude":37.41909187499999,
        "precision":163
    },
    "address":"г Москва, п Щаповское, п Курилово, ?, 52 км",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  }
]
~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/locator/v2/nearest/cluster</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: application/json;charser=UTF-8 - формат ответа JSON</li>
        </ul>
    </li>
</ul>


<ul class="nestedList params">
    <li><h3>Параметры</h3><span>Параметры передаются в строке запроса</span>
    </li>
</ul>

Параметр|Описание|Тип|Обяз.
---------|--------|---|------
latNW | Широта | Double|+
lngNW | Долгота | Double|+
zoom | Масштаб % | Integer |-
ttpId | Отбор по типу терминала: `19` - терминал партнера; `4` - терминал QIWI | Long|-
activeWithinMinutes | Активность в течение последних X минут |Long|-
withRefillWallet| Возможность пополнения кошелька |Boolean|-



<h3 class="request">Ответ ←</h3>

~~~json
[
  {
    "terminalId":10352688,
    "ttpId":4,
    "lastActive":"2017-09-20T12:10:34.288",
    "count":7,
    "coordinate": {
        "latitude":55.6869467142857,
        "longitude":37.385664,
        "precision":58
    },
    "address":"Одинцовский р-н, д Немчиново, ?, 76",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  },
  {
    "terminalId":10356000,
    "ttpId":4,
    "lastActive":"2017-09-20T12:10:47.679",
    "count":16,
    "coordinate":
      {
        "latitude":55.690496687499994,
        "longitude":37.41909187499999,
        "precision":163
      },
    "address":"г Москва, п Щаповское, п Курилово, ?, 52 км",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  }
]
~~~

Параметр|Описание|Тип
---------|--------|---
address | Адрес терминала|String
cardAllowed | Прием карт |Boolean
cashAllowed | Прием наличных |Boolean
coordinate | Объект координат |Object
coordinate.latitude | Широта |Double
coordinate.longtitude | Долгота |Double
coordinate.precision | Погрешность, в метрах |Double
count | Количество терминалов в ближайшей окрестности данных координат |Integer
description | Описание терминала. Может содержать время работы и прочие данные |String
label | Название терминала |String
lastActive | Время последней активности |Number
terminalId| Номер терминала |Long
ttpId| Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long
verified | Адрес терминала верифицирован и является актуальным |Boolean


## Поиск по полигону {#areas-search}

Поиск терминалов в пределах полигона по заданным координатам полигона.


<aside class="notice">
Если диагональ полигона больше 100 км и при этом zoom больше 12, то сработает ограничение и запрос выполнится с ошибкой
</aside>

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/locator/v2/nearest/clusters?latNW=57.05930421115318&lngNW=59.97245277050781&latSE=56.60762621886134&lngSE=61.20154822949221&zoom=10'

HTTP/1.1 200 OK
Content-Type: text/json

[
  {
    "terminalId":10321926,
    "ttpId":4,
    "lastActive":"2017-09-08T06:55:55.402",
    "count":3,
    "coordinate": {
        "latitude":57.12440766666666,
        "longitude":60.06412733333334,
        "precision":470
    },
    "address":"",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  },
  {
    "terminalId":10145713,
    "ttpId":4,
    "lastActive":"2017-09-20T19:34:56.686",
    "count":1,
    "coordinate": {
      "latitude":57.069049,
      "longitude":59.936269,
      "precision":0
    },
    "address":"г Новоуральск, д Починок, Советская ул, 2",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  }
]
~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/locator/v2/nearest/clusters</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: application/json;charset=UTF-8 - формат ответа JSON</li>
        </ul>
    </li>
</ul>


<ul class="nestedList params">
    <li><h3>Параметры</h3><span>Параметры передаются в строке запроса</span>
    </li>
</ul>

Параметр|Описание|Тип|Обяз.
---------|--------|---|------
latNW | Широта северо-западной точки полигона | Double|+
lngNW | Долгота северо-западной точки полигона| Double|+
latSE | Широта юго-восточной точки полигона| Double|+
lngSE | Долгота юго-восточной точки полигона| Double|+
zoom | Масштаб | Integer |-
ttpId | Отбор по типу терминала: `19` - терминал партнера; `4` - терминал QIWI | Long|-
activeWithinMinutes | Активность в течение последних X минут |Long|-
withRefillWallet| Возможность пополнения кошелька |Boolean|-



<h3 class="request">Ответ ←</h3>

~~~json
[
  {
    "terminalId":10321926,
    "ttpId":4,
    "lastActive":"2017-09-08T06:55:55.402",
    "count":3,
    "coordinate": {
        "latitude":57.12440766666666,
        "longitude":60.06412733333334,
        "precision":470
    },
    "address":"",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  },
  {
    "terminalId":10145713,
    "ttpId":4,
    "lastActive":"2017-09-20T19:34:56.686",
    "count":1,
    "coordinate": {
      "latitude":57.069049,
      "longitude":59.936269,
      "precision":0
    },
    "address":"г Новоуральск, д Починок, Советская ул, 2",
    "verified":true,
    "label":"QIWI",
    "description":null,
    "cashAllowed":false,
    "cardAllowed":false
  }
]
~~~

Параметр|Описание|Тип
---------|--------|---
address | Адрес терминала |String
cardAllowed | Прием карт |Boolean
cashAllowed | Прием наличных |Boolean
coordinate | Объект координат |Object
coordinate.latitude | Широта |Double
coordinate.longtitude | Долгота |Double
coordinate.precision | Погрешность |Double
count | Количество терминалов в ближайшей окрестности данных координат  |Integer
description | Описание терминала. Может содержать время работы и прочие данные |String
label | Название терминала |String
lastActive | Время последней активности |Number
terminalId| Номер терминала |Long
ttpId| Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long
verified | Адрес терминала верифицирован и является актуальным |Boolean



<a href="#" onclick="history.back(); return false">Назад</a>
