<h1>DOM.ru offers documentation (ММП)</h1>

Вопросы:

    /*
        1) type и mode - не нужно - colorLabels (personalOfferTypes для сайта), время акции туда же в массив
        6) offer-seen надо добавить (но у сайта 1 запрос по переходам по шагам) дергается когда в детальну страницу проваливается. На сайте другой запрос
    */ 

<h2> GET /channel/info </h2>
Получение информации по id канала

Просто открываете ChannelDetailsFragment (если говорить про android) передав ему channelId всё остальное он подтянет и отобразит сам

Input:
```
{
    "id": int //id канала
}
```

Output:
```
{
  "id": int,
  "title": string,
  "image": url_string,
  "themeId": int,
  "description": string,
  "url": url_string,
  "button": int,
}
```

<h2> GET /spec-offer </h2>
Получение оферов

Headers:
```
providerId: int,
systemId: string //Идентификатор системы МП 15 - iOS, 16 - Android
```

Input:
```
no input
```

Output:
```
[
    {
        "id": int,
        "name": string,
        "description": string,
        "shortDescription": string,
        "promoTime": int, //days count
        "state": int, //stepId
        "image": url_string, //картинка спецпредложения в списке
        "images: [ url_string, ... ], //картинки (слайдер) спецпредложения в детальной
        "paySum": int,
        "textColor": string, //html color code - цвет текста на карточке
        "backgroundColor": string, //html color code - цвет фона на карточке
        "paySum": int, //Сумма, которой не хватает на балансе чтобы активировать СП (для сп Оптом дешевле)
        "closeDate": string, //Дата, до которой будет подключено спецпредложение если подключить сейчас (присутствует у спецпредложений с макс. сроком действия)
        "closeDateMin":	string, //Минимальная дата, с которой можно будет отключить спецпредложение (заполнено у спецпредложений с мин.сроком действия)
        "isActiveNextButton": boolean //Флаг, активна ли кнопка перехода к следующему шагу, по умолчанию true
        "autorenewal": boolean,
        "requestId": int,
        "cost": {
            "full": int, //int for devision by 100
            "withDiscount": int, //int for devision by 100
            "discDescription": string
        },
        "features": [
            {
                "title": string,
                "icon": url_string,
            },
            ...
        ],
        "channels": [
            {
                "id": int,
                "title": string,
                "image": url_string,
                "themeId": int
            },
            ...
         ],
        "terms": {
            "description": string,
            "pdf": url_string,
        },
        "colorLabels": [ //Акция, Промо-цена, Новинка
            {
                "text": string,
                "textColor": string, //html color code
                "color": string, //html color code
                "type": string, //or int??
            },
            ...
        ],
        "childOffers": [<personalOffers Object>]
    }
]
```

<h2> POST /spec-offer/seen </h2>
Просмотр оффера

Дергается при открытии деталки по офферу

Headers:
```
providerId: int
```

Input:
```
{
    "id": int, //id спецпредложения
}
```

Output:

```
success:
{
  "result": 1
}
fail:
{
  "billingCode": "UNKNOWN",
  "message": "Неизвестная ошибка"
}
```

<h2> POST /spec-offer/activate </h2>
Активация оффера

Headers:
```
providerId: int
```

Input:
```
{
    "id": int, //id спецпредложения
    "requestId": int, //Идентификатор заявки спецпредложения
    "autorenewal": int, //Автоматическое подключение после окончания срока его действия: 0 - не подключать(по умолчанию), 1 - подключать
    "stepId": int, //Текущий шаг спецпредложения: Не просмотрено - 1348, Просмотрено - 1346, Подключено - 1344, Отключено - 1352
    "childId": int, //id дочерней акции
    "phone": string, //телефон абонента
    "contactId": int //id контактного телефона при оформлении заявки на подключение оффера на смену тарфиа или продажу об-ия
}
```

Output:

```
success:
{
  "result": 1
}
fail:
{
  "billingCode": "UNKNOWN",
  "message": "Неизвестная ошибка"
}
```

<h2> POST /spec-offer/deactivate </h2>
Деактивация оффера

Headers:
```
providerId: int
```

Input:
```
{
    "id": int, //id спецпредложения
}
```

Output:

```
success:
{
  "result": 1
}
fail:
{
  "billingCode": "UNKNOWN",
  "message": "Неизвестная ошибка"
}
```

<h2> GET /spec-offer/not-interesting/ </h2>
Мне это не интересно - получение вариантов ответа

Headers:
```
providerId: int
```

Input:
```
no input
```

Output:

```
{
    "quizAnswers": [
        {   
            "id": int,
            "title": string
        },
        ...
    ]
}
```

<h2> PUT /spec-offer/not-interesting/offer_id </h2>
Мне это не интересно - отправка ответа

Input:
```
{
    "quizAnswerId": int, //или None, если Другое
    "otherText": string //или None, если есть quizAnswerId
}
```

Output:

```
no output, only http status code
```