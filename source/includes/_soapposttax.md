## PostTax

The PostTax method can be used to modify the state of a document saved to the AvaTax database via SalesInvoice, ReturnInvoice or PurchaseInvoice methods.

**Note:** PostTax can be used to Commit a document or even change the Document Code (invoice number).

See <a href="/api-docs/designing-your-integration/posttax-and-committax">Committing Documents</a> for more details.

### PostTax Request

Input for PostTax for posting or committing a previously saved document.

#### Properties

**Commit:** bool, *optional*

If set to True, AvaTax will Post and Commit the document in one call.

**CompanyCode:** string [25], *required*

The client application company reference code.

**DocCode:** string [50], *required*

The internal reference code (invoice number) used by the client application.

**DocDate:** date, *required*

The Document Date, i.e. the date on the invoice, purchase order, etc.

**DocType:** DocumentType, *required*

The original document's type, such as Sales Invoice or Purchase Invoice

**NewDocCode:** string [50], *optional*

New Document Code for the document if desired.

**TotalAmount:** decimal, *required*

The total amount (not including tax) for the document.

**TotalTax:** decimal, *required*

The total tax for the document.

### PostTax Result

Result data returned from PostTax.

#### Properties

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request. Properties defined in <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string

The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.
