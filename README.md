<h1>DOM.ru offers documentation</h1>

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
    "personal_offers": [
        {
            "id": int,
            "title": string,
            "description": string,
            "typeId": int,
            "promoTime": int, //days count
            "listImage": url_string,
            "detailImage: url_string,
            "price": int, //int for devision by 100
            "features": [
                {
                    "title": string,
                    "icon": url_string,
                },
                ...
            ],
        }
    ]
}
```

<h2> PUT /personal-offer-buy/offer_id </h2>

Input:
```
no input
```

Output:

```
no output, only http status code
```

<h2> GET /personal-offer-not-interesting/ </h2>

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

<h2> PUT /personal-offer-not-interesting/offer_id </h2>

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