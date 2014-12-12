## EstimateTax

Retrieves tax rate details for the supplied geographic coordinates and sale amount.
Since the REST API does not provide an explicit ping function, this method can also be used to test connectivity to the service.

```curl
curl --user 1234567890:A1B2C3D4E5F6G7H8 "https://development.avalara.net/1.0/tax/47.627935,-122.51702/get?saleamount=10"
```

```java
// Required Request Parameters
Double latitude = 47.627935;
Double longitude = -122.51702;
Double saleAmount = 10.0;
//Create query/url
String queryparams = address.toQuery();
String taxest = svcURL+ "/1.0/tax/" +
	latitude.toString() + "," +
	longitude.toString() + 
	"/get?saleamount=" + 
	saleAmount.toString();
URL url;

HttpURLConnection conn;

//Connect to specified URL 
//with authorization header
url = new URL(taxest);
conn = (HttpURLConnection)url.openConnection();

//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber + ":"+licenseKey).getBytes()));

//Add authorization header
conn.setRequestProperty ("Authorization", encoded);
conn.disconnect();

//Deserialization object
ObjectMapper mapper = new ObjectMapper();
ValidateResult vres = mapper.readValue(
	conn.getInputStream(),
	ValidateResult.class);
```

```csharp
decimal latitude = (decimal)47.627935;
decimal longitude = (decimal)-122.51702;
decimal saleAmount = (decimal)10;
// Call the service
Uri address = new Uri(
	svcURL + "tax/" + latitude.ToString()+
	"," + longitude.ToString() + 
	"/get.xml?saleamount=" + saleAmount);
HttpWebRequest request = 
	WebRequest.Create(webAddress) 
	as HttpWebRequest;
request.Headers.Add(
	HttpRequestHeader.Authorization, 
	"Basic " + Convert.ToBase64String(
		ASCIIEncoding.ASCII.GetBytes(
			accountNum + ":" + license)));
request.Method = "GET";

WebResponse response = 
	request.GetResponse();
```

```php
$latitude = 47.627935;
$longitude = -122.51702;
$saleAmount = 10;

$estimateTaxRequest = new EstimateTaxRequest($latitude, $longitude, $saleAmount);
 
$url =  $this->config['url'].'/1.0/tax/'.
   $estimateTaxRequest->getLatitude().",".
   $estimateTaxRequest->getLongitude().
   '/get?saleamount='.
   $estimateTaxRequest->getSaleAmount();
$curl = curl_init();
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, 
	$this->config['account'].":".
	$this->config['license']);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER,	1);

$curl_response = curl_exec($curl);

EstimateTaxResult::parseResult($curl_response);      
```


> The above command returns JSON structured like this:

```json
{
    "Rate": 0.087,
    "Tax": 0.87,
    "TaxDetails": [
        {
            "Country": "US",
            "Region": "WA",
            "JurisType": "State",
            "Rate": 0.065,
            "Tax": 0.65,
            "JurisName": "WASHINGTON",
            "TaxName": "WA STATE TAX"
        },
        {
            "Country": "US",
            "Region": "WA",
            "JurisType": "City",
            "Rate": 0.022,
            "Tax": 0.22,
            "JurisName": "BAINBRIDGE ISLAND",
            "TaxName": "WA CITY TAX"
        }
    ],
    "ResultCode": "Success"
}
```

### URL and Method

URL: /1.0/tax/get GET

For development, 
	https://development.avalara.net
	/1.0/tax/get
    
For production, 
	https://avatax.avalara.net
	/1.0/tax/get
    
Note that xml-encoded requests should use /1.0/tax/get.xml

### Headers

**Request Method:** HTTP POST

**Authorization:** header, *required*

In the format "Basic[account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication">basic access authentication</a>.

Sample: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=

**Content Type:** header, *required*

Standard content type header, indicating the content type of the request content.

**Content Length:** header, *required*

Standard content length header, indicating the size of the request content.

### EstimateTax Request

Retrieves tax rate details for the supplied US geographic coordinates and sale amount.

#### Properties

**Latitude:** decimal, *required*

The latitude of the geographic coordinates to get tax for based on the sale amount

**Longitude:** decimal, *required*

The longitude of the geographic coordinates to get tax for based on the sale amount

**SaleAmount:** decimal, *required*

The amount of sale requiring tax calculation, in decimal format

### EstimateTax Result

Output for tax/get GET showing the retrived tax details and calculation.

#### Properties

**Rate:** decimal

Total effective tax rate

**Tax:** decimal

Total calculated tax amount

**TaxDetails:** TaxDetail[]

Tax calculation details for each jurisdiction.

**ResultCode:** SeverityLevel

SeverityLevel as per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**Messages:** Message[]

As per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

### TaxDetail

Tax details by jurisdiction.

#### Properties

**Country:** string [2]

Country of tax jurisdiction

**JurisName:** string [200]

Name of tax jurisdiction

**JurisType:** string [9]

Regional type of tax jurisdiction

**Rate:** decimal

Effective tax rate for tax jurisdiction

**Region:** string [3]

Region of tax jurisdiction

**Tax:** decimal

Tax amount

**TaxName:** string [75]

Tax name