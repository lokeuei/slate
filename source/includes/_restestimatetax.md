## EstimateTax

Retrieves tax rate details for the supplied geographic coordinates and sale amount.
Since the REST API does not provide an explicit ping function, this method can also be used to test connectivity to the service.

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