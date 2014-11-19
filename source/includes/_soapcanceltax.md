## CancelTax

Voids or deletes and existing transaction record from the AvaTax system.

### CancelTax Request

Input for CancelTax indicating the document that should be cancelled and the reason for the operation.

#### Properties

**CompanyCode:** string [25], *required*

Client application company reference code.  Not required if the document is identified by DocId.

**DocType:** enum as string [see below], *required*

Value describing what type of tax document is being cancelled. One of:

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice

Not required if the document is identified by DocId.

**DocCode:** string [50], *required*

Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  Not required if the document is identified by DocId.

**CancelCode:** enum as string [see below], *required*

The reason for cancelling the tax record. One of:

* Unspecified
* PostFailed
* DocDeleted
* DocVoided
* AdjustmentCancelled

For more information, see the <a title="CancelTax" href="/api-docs/api-reference/canceltax" target="_blank">CancelTax article</a>.

**DocId:** bigint as string, *optional*

Avatax-assigned unique Document Id, can be used in place of DocCode, DocType, and CompanyCode

### CancelTax Result

Output for CancelTax indicating the success of the cancellation, or any errors encountered.

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

**DocId:** bigint as string

The unique numeric identifier (Document ID) assigned to the tax document in question by the AvaTax Service.