## Authentication
Avalara uses API keys to allow access to the API. 
The API key is issued upon registering for an account. 

<aside class='notice'> A TaxRates API Key is required to call this service. </aside>

You can get an API key at our [developer portal](http://getrates-dev.avlr.sh/).

### Via Authorization Header:
Avalara expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: AvalaraApiKey meowmeowmeow`

where `meowmeowmeow` is replaced with your personal API key.

### Alternate Method: 
You can pass the API key in the querystring as one of the parameters instead of 
passing it in a header. i.e:

 `https://tax-dev.avlr.sh/api/rates?Line1=435+Ericksen+Ave+NE&City=Bainbridge%20Island&Region=WA&PostalCode=98110&apikey=meowmeowmeow`

where `meowmeowmeow` is replaced with your personal API key.
