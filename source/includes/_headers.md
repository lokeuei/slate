## Headers
```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: AvalaraApiKey meowmeowmeow" \
  -H "Content-Type: text/json" \
  -H "Accept: text/json" \
  -D "{ some_request_data }"
```
```ruby
require 'rest-client'
result = RestClient.post "api_endpoint_here", 
    "{ some_request_data }", 
    :authorization => 'AvalaraApiKey meowmeowmeow', 
    :content_type => 'text/json',
    :accept => 'text/json'
```

> Make sure to replace `meowmeowmeow` with your API key.

### Authentication
Avalara uses API keys to allow access to the API. 
The API key is issued upon registering for an account. 
You can get an API key at our [developer portal](http://getrates-dev.avlr.sh/).

#### Via Authorization Header:
Avalara expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: AvalaraApiKey meowmeowmeow`

where `meowmeowmeow` is replaced with your personal API key.

#### Alternate Method: 
If you are using a free TaxRates account, you can pass the API key in the querystring as one of the parameters instead of 
passing it in a header. i.e:

 `https://tax-dev.avlr.sh/api/rates?Line1=435+Ericksen+Ave+NE&City=Bainbridge%20Island&Region=WA&PostalCode=98110&apikey=meowmeowmeow`

where `meowmeowmeow` is replaced with your personal API key.

### Content Type
The `Content-Type` header is required for all POST requests. If this header is omitted, the request will result in an error.
Valid accepted values are `text\json` and `text\xml`

### Accept
The `Accept` header is optional. If no `Accept` header is specified, the service will respond with `text\json`.
If used, valid values are `text\json` and `text\xml`.
