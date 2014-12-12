## CancelTax

Voids or deletes and existing transaction record from the AvaTax system.

```curl
curl "https://development.avalara.net
	/1.0/tax/cancel" 
--user 1234567890:A1B2C3D4E5F6G7H8
--header "Content-Type: text/json" 
--data @/Docs/cancelTaxRequest.json

{
"CompanyCode":"APITrialCompany",
"DocType":"SalesInvoice",
"DocCode":"INV001",
"CancelCode":"DocVoided"
}
```

```csharp
var cancelTaxRequest = 
	new CancelTaxRequest{
	  CompanyCode = "APITrialCompany",
	  DocType = DocumentType.SalesInvoice,
	  DocCode = "INV001",
	  CancelCode = CancelCode.DocVoided
};

//Convert the request to XML
XmlSerializerNamespaces namesp = new XmlSerializerNamespaces();
namesp.Add("", ""); 
XmlWriterSettings settings = new XmlWriterSettings();
settings.OmitXmlDeclaration = true;
XmlSerializer x = new XmlSerializer(cancelTaxRequest.GetType());
StringBuilder sb = new StringBuilder();
x.Serialize(XmlTextWriter.Create(sb, settings), cancelTaxRequest, namesp);
XmlDocument doc = new XmlDocument();
doc.LoadXml(sb.ToString());

//Call the service
Uri address = new Uri(serviceURL + "/1.0/tax/cancel");
HttpWebRequest request = WebRequest.Create(address)as HttpWebRequest;

//Add Authorization header
request.Headers.Add(
	HttpRequestHeader.Authorization, 
	"Basic " + Convert.ToBase64String(ASCIIEncoding.ASCII.GetBytes(accountNumber + ":" + licenseKey)));
request.Method = "POST";
request.ContentType = "text/xml";
request.ContentLength = sb.Length;
Stream newStream = request.GetRequestStream();
newStream.Write(ASCIIEncoding.ASCII.GetBytes(sb.ToString()), 0, sb.Length);

WebResponse response = request.GetResponse();
```

```java
CancelTaxRequest cancelTaxRequest = new CancelTaxRequest();
cancelTaxRequest.CompanyCode = "APITrialCompany";
cancelTaxRequest.DocType = TaxSvc.DocType.SalesInvoice;
cancelTaxRequest.DocCode = "INV001";
cancelTaxRequest.CancelCode = CancelCode.DocVoided;

//Create URL
String target = serviceURL + "/1.0/tax/cancel";
URL url;
HttpURLConnection conn;

//Connect to URL with authorization header, request content.
url = new URL(target);
conn = (HttpURLConnection)url.openConnection();
conn.setRequestMethod("POST");
conn.setDoOutput(true);
conn.setDoInput(true);
conn.setUseCaches(false);
conn.setAllowUserInteraction(false);

//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber + ":" + licenseKey).getBytes()));
//Add authorization header
conn.setRequestProperty("Authorization", encoded);
conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");

ObjectMapper mapper = new ObjectMapper();
mapper.setSerializationInclusion(Include.NON_NULL);
//Tells the serializer to only include
//those parameters that are not null
String content = mapper.writeValueAsString(cancelTaxRequest);

//Uncomment to see the content of the
//request object
//System.out.println(content);
conn.setRequestProperty("Content-Length", Integer.toString(content.length()));

DataOutputStream wr = new DataOutputStream(conn.getOutputStream());
wr.writeBytes (content);
wr.flush ();
wr.close ();

conn.disconnect();
CancelTaxResponse res = mapper.readValue(conn.getInputStream(), CancelTaxResponse.class);

```

```php
$cancelTaxRequest = new CancelTaxRequest();
$cancelTaxRequest->setCompanyCode("APITrialCompany");
$cancelTaxRequest->setDocType(DocumentType::$SalesInvoice);		
$cancelTaxRequest->setDocCode("INV001");		
$cancelTaxRequest->setCancelCode(CancelCode::$DocVoided);

$url = $serviceURL."/1.0/tax/cancel";
$curl = curl_init($url);
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, $accountNumber.":".$licenseKey);

curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, json_encode($cancelTaxRequest)); 
$curl_response = curl_exec($curl);
curl_close($curl);

CancelTaxResult::parseResult($curl_response);
```
> The above command returns JSON structured like this:

```json
{
"CancelTaxResult": {
"TransactionId": 437966608,
"ResultCode": "Success",
"DocId": "34067366"}
}
```

### URL and Method

URL: /1.0/tax/cancel POST

For development, 
	https://development.avalara.net
	/1.0/tax/cancel
    
For production, 
	https://avatax.avalara.net
	/1.0/tax/cancel
    
Note that xml-encoded requests should use /1.0/tax/cancel.xml

### Headers

**Request Method:** HTTP POST

**Authorization:** header, *required*

In the format "Basic[account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication">basic access authentication</a>.

Sample: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=

**Content Type:** header, *required*

Standard content type header, indicating the content type of the request content.

**Content Length:** header, *required*

Standard content length header, indicating the size of the request content.

### CancelTaxRequest

Input for CancelTax indicating the document that should be cancelled and the reason for the operation.

#### Properties

**CompanyCode:** string [25], *required*

Client application company reference code.  Not required if the document is identified by DocId.

**DocType:** string, *required*

Value describing what type of tax document is being cancelled. One of:

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice

Not required if the document is identified by DocId.

**DocCode:** string [50], *required*

Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  Not required if the document is identified by DocId.

**CancelCode:** string, *required*

The reason for cancelling the tax record. 

* Unspecified
* PostFailed
* DocDeleted
* DocVoided
* AdjustmentCancelled

For more information, see <a href="/api-docs/designing-your-integration/canceltax" target="_blank">Voiding Documents</a>.

**DocId:** string, *optional*

Avatax-assigned unique Document Id, can be used in place of DocCode, DocType, and CompanyCode

### CancelTaxResult

#### Properties

**TransactionId:** string

The unique numeric identifier of the API operation assigned by the AvaTax service.

**DocId:** string

The unique numeric identifier (Document ID) assigned to the tax document in question by the AvaTax Service.

**ResultCode:** SeverityLevel

SeverityLevel as per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**Messages:** Message[]

As per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>
