<h1>DOM.ru offers documentation</h1>

<h2> GET /channel/info </h2>

Input:
```
{
    "providerId": int,
    "Domain": string,
    "id": int
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

<h2> GET /personal-offers </h2>

Input:
```
{
    "userId": int
}
```

Output:
```
{
    "personal_offer_types": [
        {
            "id": int,
            "title": string,
            "colorText": string, //html color code
            "colorBg": string, //html color code

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
    "personal_offers": [
        {
            "id": int,
            "title": string,
            "description": string,
            "typeId": int,
            "promoTime": int, //days count
            "listImage": url_string,
            "detailImage: url_string,
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
                    "icon": url_string,
                    "themeId": 1
                },
                ...
             ],
            "offer_condition": {
                "description": string,
                "pdf": url_string,
            }
        }
    ]
}
```

<h2> PUT /personal-offers-buy/offer_id </h2>

Input:
```
no input
```

Output:

```
no output, only http status code
```

<h2> GET /personal-offers-not-interesting/ </h2>

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

<h2> PUT /personal-offers-not-interesting/offer_id </h2>

Input:
```
{
    "quizAnswerId": int
}
```

Output:

```
no output, only http status code
```

<h2> GET /personal-offers-onboarding </h2>

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