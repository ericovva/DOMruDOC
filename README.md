<h1>DOM.ru offers documentation</h1>

Вопросы:

    /*
        1) type и mode
        2) state - это где вообще? это то же, что stepId в активации?
        3) requestId откуда берется?
        4) зачем передавать type в активацию?
        5) зачем нужны другие эндпоинты по спецпредложениям, которые не описаны в этой доке?
    */ 

<h2> GET /channel/info </h2>
Получение информации по id канала

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

Input:
```
{
    "userId": int
}
```

Output:
```
{
    "personalOfferTypes": [ //Акция, Промо-цена, Новинка
        {
            "id": int,
            "title": string,
            "textColor": string, //html color code
            "backgroundColor": string, //html color code

        },
        ...
    ],
    "channelThemes": [
        {
            "id": int,
            "title": string,
        },
        ...
    ],
    "personalOffers": [
        {
            "id": int,
            "name": string,
            "description": string,
            "type": int, //или mode??
            "promoTime": int, //days count
            "image": url_string, //картинка спецпредложения в списке
            "detailImage: url_string, //картинка спецпредложения в детальной
            "paySum": int,
            "textColor": string, //html color code - цвет текста на карточке
            "backgroundColor": string, //html color code - цвет фона на карточке
            "cost": {
                "full": int, //int for devision by 100
                "withDiscount": int //int for devision by 100
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
                    "themeId": 1
                },
                ...
             ],
            "terms": {
                "description": string,
                "pdf": url_string,
            }
        }
    ]
}
```

<h2> PUT /spec-offer/activate </h2>
Активация оффера

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

<h2> PUT /spec-offer/deactivate </h2>
Деактивация оффера

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

<h2> GET /spec-offer/onboarding </h2>
Получение контента для отображения слайдов онбординга

Input:
```
no input
```

Output:

```
{
    "slides": [
        {
            "title": string,
            "description": string
        },
        ...
    ]
}
```