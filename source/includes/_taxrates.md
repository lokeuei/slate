# TaxRates
> The rate limiting means that you get 60 calls per minute and ~ calls per month.

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
   ],
   "workflowDuration":1535,
   "overallDuration":6018,
   "processingWorkflowId":"a4c86c6b5b0211e4bcab001c423a9e8c"
}
```
The TaxRate API is a free, rate-limited resource that allows users to retrieve a tax rate for a street address or zip code.

### HTTP Request

`GET http://api.taxrates.avalara.com/address?<address>`

### Query Parameters

The address can be identified by either: 

 * `country` and `zipcode`
 
 * `country`, `street`, and `state`
 
 Some parameters have synonyms provided for regional translation. Only one of these synonyms should be used at a time.
 For example, a request could contain either `city` or `town`, but not both.
 

| Parameter | Description                                                  | Example            |
|---------|----------|----------|--------------------------------------------------------------|--------------------|
| street  | first line of the address           | "1101 Alaskan Way" |
| city, municipality, town    | city of the address                 | "Seattle", "Montreal", "Bournemouth" |
| state, province   | state  or region of the address       | "WA", "QC", "Washington", "Quebec" |
| country | country code in ISO 3166-1 alpha-3 format   | "USA", "CAN", "GBR"      |
| zipcode, postCode, postalCode | zip code of the address             | "98101", "V8X 3X4", "BH1 1AA" |


### Response Attributes

Attribute | Type | Description
----------|------|-------
totalRate | double | Contains the total tax rate for the location in question. Note that it is not a percentage; in the example above, the totalRate of 0.086 represents a tax rate of 8.6%.
rates | rate array | Each object in the rates array represents a single jurisdiction's contribution to the totalRate.
rate.rate | double | Note that a rate field may not always be present; in these cases, the contribution is 0.0%.
rate.name | string | TBD
rate.type | string | TBD
workflowDuration | integer | TBD
overallDuration | integer | TBD
processingWorkflowId | string | TBD
