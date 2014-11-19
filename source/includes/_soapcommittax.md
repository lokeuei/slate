## CommitTax

CommitTax is only necessary if you need to temporarily store your documents in the Avalara database in a Posted state and later commit the documents. This will require successive calls to GetTax, PostTax and CommitTax. See <a href="/api-docs/designing-your-integration/posttax-and-committax">Committing Documents</a> for more details.

### CommitTax Request

Input for CommitTax indicating the document that should be committed. You may use just the DocId to locate and commit the document (5.8 adapter and earlier, or 14.2 and later), or you may use all three of CompanyCode, DocType and DocCode.

#### Properties

**CompanyCode:** string [25], *required**

Client application company reference code.  

*Not required if the document is identified by DocId.

**DocType:** enum as string [see below], *required**

Value describing what type of tax document is being committed. One of:

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice

*Not required if the document is identified by DocId.*

**DocCode:** string [50], *required*

Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  

*Not required if the document is identified by DocId.*

**DocId:** bigint as string, *optional*

Avatax-assigned unique Document Id, can be used in place of CompanyCode, DocType and DocCode.

### CommitTax Result

Output for CommitTax indicating the success of the operation, or any errors encountered.

#### Properties

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