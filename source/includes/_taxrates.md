# TaxRates API

## Rates by Street Address

```shell
curl "https://api.taxrates.avalara.com/address?Line1=435+Ericksen+Ave+NE&City=Bainbridge%20Island&Region=WA&PostalCode=98110" \
  -H "Authorization: AvalaraApiKey meowmeowmeow"
```

```ruby
require 'json'
require 'net/http'
uri = URI("https://api.taxrates.avalara.com/address?Line1=435+Ericksen+Ave+NE&City=Bainbridge%20Island&Region=WA&PostalCode=98110")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_PEER
result = http.get(uri.request_uri, 
    'Authorization' => 'AvalaraApiKey meowmeowmeow')
JSON.parse(result.body)
```

> The above command returns JSON structured like this:

```json
{ 
   "totalRate":9.500000,
   "rates":[ 
      { 
         "rate":3.00000,
         "name":"SEATTLE",
         "type":"City"
      },
      { 
         "rate":6.500000,
         "name":"WASHINGTON",
         "type":"State"
      }
   ]
}
```

### HTTP Request

`GET http://api.taxrates.avalara.com/address?<address>`

### Query Parameters 

| Parameter | Required | Description                                                  | Example            |
|---------|----------|----------|--------------------------------------------------------------|
| street  | Required | first line of the address           | "1101 Alaskan Way" |
| city  | Optional  | city of the address                 | "Seattle", "Montreal", "Bournemouth" |
| state  | Required | state  or region of the address       | "WA", "QC", "Washington", "Quebec" |
| country | Required | country code in ISO 3166-1 alpha-3 format   | "USA", "CAN", "GBR"      |
| postal | Optional | zip code of the address             | "98101", "V8X 3X4", "BH1 1AA" |


### Response Attributes

Attribute | Type | Description
----------|------|-------
totalRate | double | Contains the total tax rate for the location in question. Note that it is not a percentage; in the example above, the totalRate of 0.086 represents a tax rate of 8.6%.
rates | rate array | Each object in the rates array represents a single jurisdiction's contribution to the totalRate.
rate.rate | double | Note that a rate field may not always be present; in these cases, the contribution is 0.0%.
rate.name | string | TBD
rate.type | string | TBD

## Rates by Zip Code

```shell
curl "https://api.taxrates.avalara.com/address?country=USA&postal=98101" \
  -H "Authorization: AvalaraApiKey meowmeowmeow" \
  -H "Accept: text/json"
```

```ruby
require 'json'
require 'net/http'
uri = URI("https://api.taxrates.avalara.com/address?country=USA&postal=98101")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_PEER
result = http.get(uri.request_uri, 
    'Authorization' => 'AvalaraApiKey meowmeowmeow')
JSON.parse(result.body)
```

> The above command returns JSON structured like this:

```json
{ 
   "totalRate":9.500000,
   "rates":[ 
      { 
         "rate":3.00000,
         "name":"SEATTLE",
         "type":"City"
      },
      { 
         "rate":6.500000,
         "name":"WASHINGTON",
         "type":"State"
      }
   ]
}
```

### HTTP Request

`GET http://api.taxrates.avalara.com/postal?<address>`

### Query Parameters

| Parameter | Required | Description                                                  | Example            |
|---------|----------|----------|--------------------------------------------------------------|
| country | Required | country code in ISO 3166-1 alpha-3 format   | "USA", "CAN", "GBR"      |
| postal | Required | zip code of the address             | "98101", "V8X 3X4", "BH1 1AA" |


### Response Attributes

Attribute | Type | Description
----------|------|-------
totalRate | double | Contains the total tax rate for the location in question. Note that it is not a percentage; in the example above, the totalRate of 0.086 represents a tax rate of 8.6%.
rates | rate array | Each object in the rates array represents a single jurisdiction's contribution to the totalRate.
rate.rate | double | Note that a rate field may not always be present; in these cases, the contribution is 0.0%.
rate.name | string | TBD
rate.type | string | TBD