## AdjustTax

AdjustTax allows you to make adjustments to existing committed documents. Be aware that modifying committed documents may lead to reconciliation issues if not properly managed. When a document is adjusted via this method, all versions of the document are stored in the Avalara database to preserve the history, but only the most recent version will appear in the admin console or on reports.

**NOTE:** If Document status is Locked (meaning Avalara has already submitted the document on a return to the tax authority), then the system will not process any AdjustTax call.


### AdjustTax Request

Input for adjusting documents. An AdjustTaxRequest consists of the body of a regular GetTaxRequest plus the addition of the AdjustTaxRequest object and calling method.

#### Properties

**AdjustmentReason:** int, *required*

Sets a valid reason for the given AdjustTax call. AdjustmentReason is a high level classification of why an Original Document is being modified. 

Options:

* 0 - Not Adjusted 
* 1 - Sourcing Issue 
* 2 - Reconciled with General Ledger 
* 3 - Exemption Certificate Applied 
* 4 - Price or Quantity Adjusted 
* 5 - Item Returned 
* 6 - Item Exchanged 
* 7 - Bad Debt 
* 8 - Other (Explain) Must provide AdjustmentDescription 

**AdjustmentDescription:** string [255], *required when AdjustmentReason is Other*

Should be used when AdjustmentReason is "Other" for enhanced traceability. Leave empty for all AdjustmentReason selections except 8 - Other.

**GetTaxRequest:** GetTaxRequest, *required*

The GetTaxRequest object that will replace the original document. All original values that aren't being modified need to be populated in this object in addition to any values that are being modified.

### AdjustTax Result

Result data returned from AdjustTax. Within this result you will find the same elements as a GetTaxResult.

It is likely you will want to consider retrieving the document Version in addition to other tax related information. This is an element of all GetTaxResult or AdjustTaxResult objects.

#### Properties

**AdjustTaxResult:** AdjustTaxResult

The AdjustTaxResult for the document. 

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request. Properties defined in <a title="Common Response Format" href="http://developer.avalara.com/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string

The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.