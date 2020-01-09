---
title: QIWI-Terminal-Map API 3.0.0

search: true

metatitle: QIWI-Terminal-Map API 3.0.0

metadescription: API Карты терминалов QIWI позволяет установить местонахождение терминалов QIWI на территории РФ.

language_tabs:
  - shell

services:



toc_footers:
  - <a href='/'>На главную</a>
  - <a href='mailto:bss@qiwi.com'>Обратная связь</a>

---

# API Карты терминалов QIWI {#qiwi-map}

###### Последнее обновление: 2018-12-07 | [Редактировать на GitHub](https://github.com/QIWI-API/qiwi-map-docs/blob/master/qiwi-map_ru.html.md)

API Карты терминалов QIWI позволяет установить местонахождение терминалов QIWI на территории РФ и отобразить их на карте Google Map или Яндекс.Карты.

<aside class="notice">
С открытым исходным кодом Javascript-приложения, использующего API карты терминалов, можно ознакомиться <a href="https://github.com/QIWI-API/qiwi-map">по ссылке</a>
</aside>

<img alt="Map" src="/images/qiwi-map.png" />

<aside class="warning">API не предназначено для выгрузки списка терминалов в файл. Точки можно отображать только на карте.</aside>


## Поиск по координатам {#area-search}

Поиск терминалов в окрестности заданных координат.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/locator/v3/nearest/clusters?latNW=55.690881&latSE=55.580184&lngNW=37.386282&lngSE=37.826078&zoom=12&withRefillWallet=true&ttpGroups[0]=4&identificationTypes[1]=2&cardAllowed=true&cacheAllowed=true'

HTTP/1.1 200 OK
Content-Type: text/json

[
    {
        "terminalId": 1000021154,
        "ttpId": 10004,
        "lastActive": "2018-11-22T14:10:04.608",
        "count": 2,
        "coordinate": {
            "latitude": 55.719384,
            "longitude": 37.781102,
            "precision": 0
        },
        "address": "Москва, Рязанский пр-т., д.2, ТЦ \"Город\", 1 этаж",
        "verified": true,
        "label": "АК БАРС БАНК",
        "description": "ежедневно с 8.30 - 22.00",
        "cashAllowed": false,
        "cardAllowed": true,
        "identificationType": 2
    }
]
~~~

<ul class="nestedList url">
    <li><h3>URL <span>http://edge.qiwi.com/locator/v3/nearest/clusters?parameters</span></h3>
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
latNW | Широта северо-западной точки полигона | Double|+
lngNW | Долгота северо-западной точки полигона | Double|+
latSE | Широта юго-восточной точки полигона | Double|+
lngSE | Долгота юго-восточной точки полигона | Double|+
zoom | Масштаб. **Для максимального zoom существует ограничение размера (диагонали) полигона в 450 метров. При каждом уменьшении зума на единицу, разрешенная диагональ полигона, увеличивается в два раза.** <br>[Подробнее про уровень масштабирования карты](https://tech.yandex.ru/maps/doc/staticapi/1.x/dg/concepts/map_scale-docpage/) | Integer |-
activeWithinMinutes | Не включать в выборку терминалы, не активные более X минут |Long|-
withRefillWallet| Включить в выборку точки партнеров для пополнения кошелька |Boolean|-
ttpIds | Фильтр по типу точки партнеров пополнения.<br>10001 - Евросеть,<br>10004 - Contact<br>10002 - Связной<br>10005 -	Киви Банк<br>10006 - Офисы КИВИ<br>10007 -	Кассы партнеров<br>10008 - Банки и Банкоматы<br>10009 - TELE2<br>**Список типов не фиксирован и может меняться. Рекомендуется использовать фильтр по группам (параметр ttpGroups)** | List<Long>|-
cacheAllowed | Фильтр по возможности приема наличных | Boolean | -
cardAllowed | Фильтр по возможности приема банковских карт | Boolean | -
identificationTypes | Фильтр по возможности прохождения идентификации.<br>0 - нет идентификации<br>1 - частичная идентификация<br>2 - полная идентификация | List<Integer> | -
ttpGroups | Фильтр по группе терминалов (группа может включать от одного до нескольких типов терминала). Список групп можно получить [отдельным запросом](#list-trms) | List<Long> | -





<h3 class="request">Ответ ←</h3>

~~~json
[
    {
        "terminalId": 1000021154,
        "ttpId": 10004,
        "lastActive": "2018-11-22T14:10:04.608",
        "count": 2,
        "coordinate": {
            "latitude": 55.719384,
            "longitude": 37.781102,
            "precision": 0
        },
        "address": "Москва, Рязанский пр-т., д.2, ТЦ \"Город\", 1 этаж",
        "verified": true,
        "label": "АК БАРС БАНК",
        "description": "ежедневно с 8.30 - 22.00",
        "cashAllowed": false,
        "cardAllowed": true,
        "identificationType": 2
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
coordinate.longitude | Долгота |Double
coordinate.precision | Погрешность, в метрах |Double
count | Количество терминалов в кластере |Integer
description | Описание терминала. Может содержать время работы и прочие данные |String
label | Название терминала |String
lastActive | Время последней активности |Number
terminalId| Номер терминала |Long
ttpId| Тип терминала | Long
verified | Адрес терминала верифицирован и является актуальным |Boolean
identificationType | 0 - нет идентификации<br>1 - частичная идентификация<br>2 - полная идентификация | Number


<a href="#" onclick="history.back(); return false">Назад</a>


## Выдача списка групп терминалов {#list-trms}

Получение справочника типов (групп) терминалов.

~~~shell
user@server:~$ curl -X GET --header 'Accept: application/json;charset=UTF-8' 'https://edge.qiwi.com/locator/v3/ttp-groups'

HTTP/1.1 200 OK
Content-Type: text/json

[
    {
        "title": "Терминалы QIWI",
        "id": 1,
        "maps": [
            "TERMINAL",
            "REPLENISH",
            "IDENTIFICATION"
        ]
    },
    {
        "title": "Терминалы партнеров",
        "id": 2,
        "maps": [
            "TERMINAL",
            "REPLENISH"
        ]
    },
    {
        "title": "Салоны связи",
        "id": 3,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Банки и банкоматы",
        "id": 4,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Пункты CONTACT",
        "id": 5,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Офисы QIWI",
        "id": 6,
        "maps": [
            "IDENTIFICATION"
        ]
    }
]
~~~

<ul class="nestedList url">
    <li><h3>URL <span>http://edge.qiwi.com/locator/v3/ttp-groups</span></h3>
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
    <li><h3>Параметры</h3><span>Параметры запроса отсутствуют</span>
    </li>
</ul>

<h3 class="request">Ответ ←</h3>

~~~json
[
    {
        "title": "Терминалы QIWI",
        "id": 1,
        "maps": [
            "TERMINAL",
            "REPLENISH",
            "IDENTIFICATION"
        ]
    },
    {
        "title": "Терминалы партнеров",
        "id": 2,
        "maps": [
            "TERMINAL",
            "REPLENISH"
        ]
    },
    {
        "title": "Салоны связи",
        "id": 3,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Банки и банкоматы",
        "id": 4,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Пункты CONTACT",
        "id": 5,
        "maps": [
            "REPLENISH"
        ]
    },
    {
        "title": "Офисы QIWI",
        "id": 6,
        "maps": [
            "IDENTIFICATION"
        ]
    }
]
~~~

Параметр|Описание|Тип
---------|--------|---
title | Название группы терминалов|String
id | Идентификатор группы  |Long

<aside class="notice">Остальная информация в ответе является служебной</aside>

<a href="#" onclick="history.back(); return false">Назад</a>
