# SOAP API

The Avalara SOAP API exposes all methods available for interacting with the AvaTax service, allowing calculation of tax, modification of documents, and validation of addresses - including some functionality not exposed by our REST API.
If you're unsure of which API to use, a full comparison of the differences between the functionality provided by our REST and SOAP interfaces is documented [here](http://developer.avalara.com/api-docs/designing-your-integration/soap-or-rest).


## URL

URL:
Development: 
	https://development.avalara.net/
 
Production: 
	https://avatax.avalara.net/



## Headers

#### Configuration

**Account:** int as string [10], *required*
The unique account number provided by Avalara for verification against the service. 
If you are on a free trial and don't have a license key, use **Username**.

**License Key:** string [16], *required*

The unique alpha-numeric key provided by Avalara for verification against the service. 
If you are on a free trial and don't have a license key, use **Password**.

**Username:** string [50], optional - using Account and License is preferred

Your AvaTax Admin Console username. Usually an email address.

**Password:** string [50], optional - using Account and License is preferred

Your AvaTax Admin Console password.

#### Profile

**Name:** string [50]

Reference to a named profile

**Client:** string [50, 50]

Client application name and version

**Adapter:** string [50, 50]

Name and version of the adapter. 
This is set automatically by the .NET, PHP, and Java adapters.

**Machine:** string [50]

The NetBIOS name of the local computer. 
This is set automatically by the .NET, PHP, and Java adapters.