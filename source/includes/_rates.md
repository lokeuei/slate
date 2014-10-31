# Rates

## Calculate Tax by Street Address

```shell
curl "https://tax-dev.avlr.sh/api/rates/usa/100%20Ravine%20Lane%20NE/Bainbridge%20Island/wa/98110"
  -H "Authorization: AvalaraApiKey meowmeowmeow"
```

```php
blah blah $ -> $ 
```

> The above command returns JSON structured like this:

```json
{
    "totalRate": 0.086000,
    "rates": [
        {
            "rate": 0.021000,
            "name": "WA CITY TAX",
            "type": "city"
         },
         {
             "rate": 0.065000,
             "name": "WA STATE TAX",
             "type": "state"
         },
         {
             "name": "WA COUNTY TAX",
             "type": "county"
         }
    ]
}
```

<aside class="notice">
This resource is rate limited ...
</aside>

This endpoint provides a tax calculation based on a street address input.
This resource provides a tax estimate of limited accuracy, and does not provide...

### HTTP Request

`GET http://api.getrates.avalara.com/api/rates?<address>`

### Query Parameters

| Parameter | Required | Description                                                  | Example            |
|---------|----------|----------|--------------------------------------------------------------|--------------------|
| line1   | Yes      | This string captures the first line of the address           | "1101 Alaskan Way" |
| line2   | No       | This string captures the second line of the address | "Suite 123"        |
| line3   | No       | This string captures the third line of the address  | "Box 123", "Framingham Pigot"  |
| city    | No       | This string captures the city of the address                 | "Seattle", "Montreal", "Bournemouth" |
| state   | No       | This string captures the state of the address       | "WA", "QC", "Washington", "Quebec" |
| country | Yes      | This string captures the country code in ISO 3166-1 alpha-3 format   | "USA", "CAN", "GBR"      |
| zipcode | Yes      | This string captures the zip code of the address             | "98101", "V8X 3X4", "BH1 1AA" |
| municipality  | No | Synonym for city                                       | "Seattle", "Montreal", "Bournemouth" |
| town    | No | Synonym for city                                             | "Seattle", "Montreal", "Bournemouth" |
| province  | No | Synonym for state                                          | "WA", "QC"            |
| postalCode | Yes   | Synonym for zipcode                                       | "98101", "V8X 3X4", "BH1 1AA"   |
| postcode | Yes   | Synonym for zipcode                                         | "98101", "V8X 3X4", "BH1 1AA"   |

## Calculate Tax by Latitude/Longitude

```shell
curl "https://tax-dev.avlr.sh/api/rates/usa/100%20Ravine%20Lane%20NE/Bainbridge%20Island/wa/98110"
  -H "Authorization: AvalaraApiKey meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "totalRate": 0.086000,
    "rates": [
        {
            "rate": 0.021000,
            "name": "WA CITY TAX",
            "type": "city"
         },
         {
             "rate": 0.065000,
             "name": "WA STATE TAX",
             "type": "state"
         },
         {
             "name": "WA COUNTY TAX",
             "type": "county"
         }
    ]
}
```

<aside class="notice">
This resource is rate limited ...
</aside>

This endpoint provides a tax calculation based on a latitude/longitude combination.

### HTTP Request

`GET http://api.getrates.avalara.com/api/rates?<latitude>,<longitude>`

### URL Parameters

| Parameter | Description                                            | Example                  |
|-----------|--------------------------------------------------------|--------------------------|
| latitude  | This decimal captures the latitude of the transaction  | 47.604813                |
| longitude | This decimal captures the longitude of the transaction | -122.339811              |



