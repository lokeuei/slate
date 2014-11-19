## GetTaxHistory

GetTaxHistory allows you to query our service to retrieve details for previously saved documents.

### GetTaxHistory Request

Input for GetTaxHistory indicating the document for which history should be retrieved. The request must specify all of CompanyCode, DocCode, and DocType in order to uniquely identify the document.

#### Properties

**CompanyCode:** string [25], *required*

Gets or sets the client application company reference code.

**DocCode:** string [50], *required*

Gets or sets the Document Code, i.e. the internal reference code used by the client application.

**DocType:** DocumentType, *required*

The original document's type, such as Sales Invoice or Purchase Invoice

**DetailLevel:** DetailLevel, *required*

Specifies the level of detail to return.

### GetTaxHistory Result

Result data returned from GetTaxHistory. You can retrieve any part of the GetTaxRequest or GetTaxResult.

#### Properties

**GetTaxRequest:** GetTaxRequest

The original GetTaxRequest for the document.

**GetTaxResult:** GetTaxResult

The original GetTaxResult for the document.

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string

The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.