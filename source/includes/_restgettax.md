## GetTax

Calculates taxes on a document such as a sales order, sales invoice, purchase order, purchase invoice, or credit memo.

### URL and Method

URL: /1.0/tax/get POST

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

### GetTaxRequest

Input for GetTax describing the document on which tax should be calculated.

#### Properties 

**BusinessIdentificationNo:** string [25], *optional, unless the user needs VAT calculated*

The buyer's VAT id. Using this value will force VAT rules to be considered for the transaction. This may be set on the document or the line.

**Commit:** bool, *optional*

Default is false. Setting this value to true will prevent further document status changes, except voiding with CancelTax.

**Client:** string [50], *optional*

An identifier of software client generating the API call.

**CompanyCode:** string [25], *optional*

The code that identifies the company in the AvaTax account in which the document should be posted. This code is declared during the company setup in the <a href="https://admin-development.avalara.net/" target="_blank">AvaTax Admin Console</a>. If no value is passed, the document will be assigned to the default company.

**CustomerCode:** string [50], *required*

The client application customer reference code. This is required since it is the key to the Exemption Certificate Management Service in the Admin Console.

**CurrencyCode:** string [3], *optional*

3 character ISO 4217 compliant currency code.

**CustomerUsageType:** string [25], *optional*

The client application customer or usage type.

The standard values for the CustomerUsageType are:

 - A - Federal Government
 - B - State/Local Govt.
 - C - Tribal Government
 - D - Foreign Diplomat
 - E - Charitable Organization
 - F - Religious/Education
 - G - Resale
 - H - Agricultural Production
 - I - Industrial Prod/Mfg.
 - J - Direct Pay Permit
 - K - Direct Mail
 - L - Other
 - N - Local Government
 - P - Commercial Aquaculture (Canada)
 - Q - Commercial Fishery (Canada)
 - R - Non-resident (Canada)
 - MED1 - US MDET with exempt sales tax
 - MED2 - US MDET with taxable sales tax

**DetailLevel:** DetailLevel, *optional*

Specifies the level of detail to return.

 - Summary - summarizes document and jurisdiction detail with no line breakout
 - Document - only document detail
 - Line - document and line detail
 - Tax - document, line and jurisdiction detail
 
 **Discount:** decimal, *optional*

The discount amount to apply to the document. This may be used along with the line attribute Discounted in order to distribute a set discount amount proportionally across the applicable document lines.

**DocCode:** string [50], *optional*

While this is an optional field, serious consideration should be given to using it. If no value is sent, AvaTax assigns a GUID value to keep the document unique. This can make reconciliation a challenge.

**DocDate:** DateTime, *required*

The date on the invoice, purchase order, etc. Format YYYY-MM-DD.

**DocType:** DocumentType

The document type specifies the category of the document and affects how the document is treated after a tax calculation.

 - SalesOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - SalesInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
 - PurchaseOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - PurchaseInvoice : The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
 - ReturnOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - ReturnInvoice: The document is a permanent sales return invoice; document and tax calculation results are saved in the tax history GetTaxResult will return with a DocStatus of Saved.


**ExemptionNo:** string [25], *optional*

Any string value will cause the sale to be exempt. This should only be used if your finance team is manually verifying and tracking exemption certificates.

**PosLaneCode:** string [50], *optional*

Permits a Point of Sale application to record the unique code / ID / number associated with the terminal processing a sale.

**PurchaseOrderNo:** string [50], *optional*

Your customer's purchase order number.

**ReferenceCode:** string [50], *optional*

For returns, refers to the DocCode of the original invoice.

**TaxOverride:** TaxOverride, *optional*

TaxOverride for the document - can be used to manually override components of the tax calculation. See TaxOverride for more information.

**Addresses:** Address, at least one required

Document address array. Should represent all origin and destination addresses which will be associated with individual lines.

**Lines:** Line, at least one required

Document line array. There is a limit of 1000 lines per document.

#### TaxOverride

Nested object describing any tax override applied to the document. TaxOverride only needs to be included when there is need to override our tax calculation. Most commonly on ReturnInvoices. For each document, this may be done at either the document or line level, but not both on the same document. 

This will probably be handled within some conditional statement like:

 - if(getTaxRequest.DocType == DocumentType.ReturnInvoice)
 - do TaxOverride


**Reason:** string [255], *required*

This provides the reason for a tax override for audit purposes. Typical reasons include: "Return", "Layaway", "Imported".

**TaxOverrideType:** string, *required*

 - None: Default

 - TaxAmount: The TaxAmount overrides the total tax for the document. This is used for imported documents, returns, and layaways where the tax has already been calculated either by AvaTax or another means.


 - Exemption: Exemption certificates are overridden making the document taxable. This may be used for situations where a normally exempt entity needs to be treated as not exempt.


 - TaxDate: The TaxDate overrides the DocDate as the effective date used for tax calculation. This may effect rates, rules and other factors.

**TaxDate:** string, *must be valid date, required if TaxOverrideType is TaxDate*

The override tax date to use. This is used when the tax has been previously calculated as in the case of a layaway, return or other reason indicated by the Reason element. If the date is not overridden, then it should be set to the same as the DocDate.

**TaxAmount:** string, *must be numeric, required if TaxOverrideType is TaxAmount*

The overriding amount of tax to apply. This is distributed across all taxable rows.

#### Line
Input property of the GetTaxRequest describing item lines.

**LineNo:** string [50], *required*

Line item identifier. LineId uniquely identifies the line item row.

**DestinationCode:** string, *required*

Destination (ship-to) address code.DestinationCode references an address from the Addresses collection.

**OriginCode:** string, *required*

Origination (ship-from) address code. OriginCode references an address from the Addresses collection.

**ItemCode:** string [50], *optional*

Your item identifier, SKU, or UPC. Strongly recommended. 

**TaxCode:** string [25], *optional*

Product taxability code of the line item. Can be an AvaTax system tax code, or a custom-defined tax code.

**CustomerUsageType:** string [25], *optional*

The client application customer or usage type. CustomerUsageType determines the exempt status of the transaction based on the exemption tax rules for the jurisdictions involved. Can also be referred to as Entity/Use Code.

**Description:** string [255], *optional*

Item description. Required for customers using our filing service.

**Qty:** decimal, *required*

Item quantity. The tax engine does NOT use this as a multiplier with price to get the Amount.

**Amount:** decimal, *required*

Total amount of item (extended amount, qty * unit price)

**Discounted:** bool, *optional*

Should be set to true if the document level discount is applied to this line item. Defaults to false.

**TaxIncluded:** bool, *optional*

Should be set to true if the tax is already included, and sale amount and tax should be back-calculated from the provided Line.Amount. Defaults to false.

**Ref1:** string [250], *optional*

Value stored with SalesInvoice DocType that is submitter dependent.

**Ref2:** string [250], *optional*

Value stored with SalesInvoice DocType that is submitter dependent.

**TaxOverride** TaxOverride, *optional*

Same as document-level TaxOverride. Use this if you only need to override individual lines.


#### Address
Input property of GetTaxRequest representing addresses needed for tax calculations.

**AddressCode:** string, *required*

Reference code uniquely identifying this address instance.

**Line1:** string [50], *required*

Address line 1, required if Latitude and Longitude are not provided.

**Line2:** string [50], *optional*

Address line 2

**Line3:** string [50], *optional*

Address line 3

**City:** string [50], *optional*

City name, required unless PostalCode is specified and/or Latitude and Longitude are provided.

**Region:** string [3], *optional*

State, province, or region name. Required unless City is specified and/or Latitude and Longitude are provided.

**Country:** string [2], *optional*

Country code. If not provided, will default to "US".

**PostalCode:** string [11], *optional unless City and Region are not specified*

Postal or ZIP code, Required unless City and Region are specified, and/or Latitude and Longitude are provided.

**Latitude:** decimal, *optional*

Geographic latitude. If Latitude is defined, it is expected that the longitude field will also be provided. Failure to do so will result in operation error.

**Longitude:** decimal, *optional*

Geographic longitude. If Longitude is defined, it is expected that the latitude field will also be provided. Fail to do so will result in operation error.

**TaxRegionId:** int, *optional*

AvaTax tax region identifier. If a non-zero value is entered into TaxRegionId, other fields will be ignored.


### GetTaxResult

#### Properties
Document-level tax calculation information.

**DocCode:** string [50]

The document code, if not supplied in the request the returned value is a GUID.

**DocDate:** date

Date of invoice, sales order, purchase order, etc.

**TimeStamp:** DateTime

Server timestamp of request.

**TotalAmount:** decimal

Sum of all line Amount values.

**TotalDiscount:** decimal

Sum of all TaxLine discount amounts.

**TotalExemption:** decimal

Total exemption amount.

**TotalTaxable:** decimal

Total taxable amount.

**TotalTax:** decimal

Sum of all TaxLine tax amounts.

**TotalTaxCalculated:** decimal

TotalTaxCalculated indicates the total tax calculated by AvaTax. This is usually the same as the TotalTax, except when a tax override amount is specified. 
This is for informational purposes. The TotalTax will still be used for reporting.

**TaxDate:** date

Date used to assess tax rates and jurisdictions.

**TaxLines:** TaxLine[]

Tax calculation details for each item line (returned for detail levels Line and Tax).

**TaxSummary:** TaxDetail[]

Summary of the jurisdiction details for all item lines (returned for detail levels Summary and Line).

**TaxDetails:** TaxDetail[]

Tax calculation details for each jurisdiction per line (returned for detail level Tax).

**TaxAddresses:** TaxAddress[]

Addresses used in tax calculations (returned for detail levels Line and Tax).

**ResultCode:** SeverityLevel

Severity as per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**Messages:** Message[]

As per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

#### TaxLine

#### TaxDetail
#### TaxAddress