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

---

# API Карты терминалов QIWI {#qiwi-map}

###### Последнее обновление: 2017-08-02 | [Редактировать на GitHub](https://github.com/QIWI-API/qiwi-map-docs/blob/master/qiwi-map_ru.html.md)

API Карты терминалов QIWI позволяет установить местонахождение терминалов QIWI на территории РФ.

<aside class="notice">
С открытым исходным кодом приложения карты терминалов можно ознакомиться <a href="https://github.com/QIWI-API/qiwi-map">по ссылке</a>
</aside>

<img src="images/qiwi-map.png" />

## Поиск по адресу {#adress-search}

Запрос выполняет поиск терминалов по заданному адресу и ряду дополнительных параметров.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/address?address=%D0%90%D0%BD%D0%B4%D1%80%D0%BE%D0%BF%D0%BE%D0%B2%D0%B0%20&page=1&ttpId=0'

HTTP/1.1 200 OK
Content-Type: text/json
{
  "page": 0,
  "pageCount": 0,
  "pageSize": 0,
  "terminals": [
    {
      "address": {
        "city": "string",
        "country": "string",
        "county": "string",
        "fullAddress": "string",
        "region": "string",
        "street": "string"
      },
      "coordinate": {
        "latitude": 0,
        "longitude": 0,
        "precision": 0
      },
      "lastActive": "2017-08-01T15:59:56.133Z",
      "terminalId": 0,
      "ttpId": 0,
      "verified": true
    }
  ]
}

~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/address</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: text/json или Accept: application/json - формат ответа JSON</li>
        </ul>
    </li>
</ul>


<ul class="nestedList params">
    <li><h3>Параметры</h3><span>Параметры передаются в строке запроса</span>
    </li>
</ul>

Параметр|Описание|Тип|Обяз.
---------|--------|---|------
address | URL encoded данные адреса терминала | String|+
page | Номер страницы в выгрузке | Long|+
ttpId | `19` - терминалы партнеров; `4` - терминалы QIWI | Long |-
verified | Адрес терминала верифицирован и является актуальным | Boolean|-
activeWithinMinutes | Активность в течении X минут |Long|-



<h3 class="request">Ответ ←</h3>


Параметр|Описание|Тип
---------|--------|---
page | Номер страницы в выдаче результатов запроса. Количество терминалов одной страницы не может превышать 1000 | String
pageCount | Количество страниц в результате запроса | Long
pageSize | Количество терминалов в одной странице. Максимальное 1000| Long
terminals | Массив найденных терминалов | Array
adress | Объект данных о терминале |Object
city | Город |String
country | Страна |String
county | Округ |String
fullAdress | Полный адрес |String
region | Регион |String
street | Улица |String
coordinate | Объект координат |Object
latitude | Широта |Double
longtitude | Долгота |Double
precision | Погрешность |Double
lastActive | Время последней активности терминала |Date
terminalId | Номер терминала |Long
ttpId | Тип терминала: `19` - терминал партнера; `4` - терминал QIWI |Number
verified | Адрес терминала верифицирован и является актуальным |Boolean

## Поиск по координатам {#area-search}

Поиск терминалов по заданным координатам.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/v2/nearest/cluster?latNW=57.05930421115318&lngNW=59.97245277050781&zoom=10'

HTTP/1.1 200 OK
Content-Type: text/json
[
  {
    "address": "string",
    "cardAllowed": true,
    "cashAllowed": true,
    "coordinate": {
      "latitude": 0,
      "longitude": 0,
      "precision": 0
    },
    "count": 0,
    "description": "string",
    "label": "string",
    "lastActive": "string",
    "terminalId": 0,
    "ttpId": 0,
    "verified": true
  }
]

~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/v2/nearest/clusters</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: text/json или Accept: application/json - формат ответа JSON</li>
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
ttpId | Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long|-
activeWithinMinutes | Активность в течение последних X минут |Long|-
withRefillWallet| Возможность пополнения кошелька |Boolean|-



<h3 class="request">Ответ ←</h3>


Параметр|Описание|Тип
---------|--------|---
address | Адрес терминала|String
cardAllowed | Прием карт |Boolean
cashAllowed | Прием наличных |Boolean
coordinate | Объект координат |Object
latitude | Широта |Double
longtitude | Долгота |Double
precision | Погрешность |Double
count | Количество терминалов на странице |Integer
description | Описание терминала. Может содержать время работы и прочие данные |String
label | Название терминала |String
LastActive | Время последней активности |Number
terminalId| Номер терминала |Long
ttpId| Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long
verified | Адрес терминала верифицирован и является актуальным |Boolean


## Поиск по полигону {#areas-search}

Поиск терминалов по заданным координатам полигона.


<aside class="notice">
Если диагональ полигона больше 100 км и при этом zoom больше 12 сработает ограничение и запрос выполнится с ошибкой
</aside>

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/v2/nearest/clusters?latNW=57.05930421115318&lngNW=59.97245277050781&latSE=56.60762621886134&lngSE=61.20154822949221&zoom=10'

HTTP/1.1 200 OK
Content-Type: text/json
[
  {
    "address": "string",
    "cardAllowed": true,
    "cashAllowed": true,
    "coordinate": {
      "latitude": 0,
      "longitude": 0,
      "precision": 0
    },
    "count": 0,
    "description": "string",
    "label": "string",
    "lastActive": "string",
    "terminalId": 0,
    "ttpId": 0,
    "verified": true
  }
]

~~~

<ul class="nestedList url">
    <li><h3>URL <span>https://edge.qiwi.com/v2/nearest/clusters</span></h3>
    </li>
</ul>

<h3 class="request method">Запрос → GET</h3>

<ul class="nestedList header">
    <li><h3>HEADERS</h3>
        <ul>
             <li>Accept: text/json или Accept: application/json - формат ответа JSON</li>
        </ul>
    </li>
</ul>


<ul class="nestedList params">
    <li><h3>Параметры</h3><span>Параметры передаются в строке запроса</span>
    </li>
</ul>

Параметр|Описание|Тип|Обяз.
---------|--------|---|------
latNW | Широва северо-западной точки | Double|+
lngNW | Долгота северо-западной точки | Double|+
latSE | Широта юго-восточной точки | Double|+
lngSE | Долгота юго-восточной точки | Double|+
zoom | Масштаб | Integer |-
ttpId | Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long|-
activeWithinMinutes | Активность в течение последних X минут |Long|-
withRefillWallet| Возможность пополнения кошелька |Boolean|-



<h3 class="request">Ответ ←</h3>


Параметр|Описание|Тип
---------|--------|---
address | Адрес |String
cardAllowed | Прием карт |Boolean
cashAllowed | Прием наличных |Boolean
coordinate | Объект координат |Object
latitude | Широта |Double
longtitude | Долгота |Double
precision | Погрешность |Double
count | Количество терминалов на странице  |Integer
description | Описание терминала. Может содержать время работы и прочие данные |String
label | Название терминала |String
lastActive | Время последней активности |Number
terminalId| Номер терминала |Long
ttpId| Тип терминала: `19` - терминал партнера; `4` - терминал QIWI | Long
verified | Адрес терминала верифицирован и является актуальным |Boolean



<a href="#" onclick="history.back(); return false">Назад</a>
