## GetTax

Calculates taxes on a document such as a sales order, sales invoice, purchase order, purchase invoice, or credit memo.

### GetTax Request

Input for GetTax describing the document on which tax should be calculated.

#### Properties

**BusinessIdentificationNo:** string [25], *optional, unless the user needs VAT calculated*

The buyer's VAT id. Using this value will force VAT rules to be considered for the transaction. 
This may be set on the document or the line.

**Commit:** bool, *optional*

Default is false. Setting this property to True will prevent any further document state changes except CancelTax which changes the state to Voided.

**CompanyCode:** string [25], *required*

The code that identifies the company in the AvaTax account in which the document should be posted. This code is declared during the company setup in the 
<a href="https://admin-development.avalara.net/" target="_blank">AvaTax Admin Console</a>. If no value is passed, the document will be assigned to the default company.

**CurrencyCode:** string [3], *optional*

3 character ISO 4217 compliant currency code

**CustomerCode:** string [50], *required*

The client application customer reference code. This is required since it is the key to the Exemption Certificate Management Service in the Admin Console.

**CustomerUsageType:** string [25], *optional*

The client customer or usage type (or Entity Use Code). 

Standard options:

* A - Federal Government
* B - State/Local Govt.
* C - Tribal Government
* D - Foreign Diplomat
* E - Charitable Organization
* F - Religious/Education
* G - Resale
* H - Agricultural Production
* I - Industrial Prod/Mfg.
* J - Direct Pay Permit
* K - Direct Mail
* L - Other
* N - Local Government
* P - Commercial Aquaculture (Canada)
* Q - Commercial Fishery (Canada)
* R - Non-resident (Canada)
* MED1 - US MDET with exempt sales tax
* MED2 - US MDET with taxable sales tax

**DestinationAddress:** Address, *required*

Address in the collection that will be used as destination or "Ship To" location in the tax calculation.

**DetailLevel:** DetailLevel, *optional*

Specifies the level of tax detail returned in the GetTaxResult.


* Summary: Summarizes document and jurisdiction detail with no line breakout
* Document: Only document detail
* Line: Document and line detail
* Tax: Document, line and jurisdiction detail
* Diagnostic: In addition to Tax level details, indicates that the server should return information about how the tax was calculated. Intended for use only while the SDK is in a development environment. 

**Discount:** decimal, *optional*

The total discount to be applied to the line or lines identified by the Lines.Discounted property.

**DocCode:** string [50], *optional*

While this is an optional field, serious consideration should be given to using it. If no value is sent, AvaTax assigns a GUID value to keep the document unique. This can make reconciliation a challenge.

**DocDate:** date, *required*

The date on the invoice, purchase order, etc. Format YYYY-MM-DD.

**DocType:** DocumentType, *required*

The document type specifies the category of the document and affects how the document is treated after a tax calculation.

* SalesOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* SalesInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
* PurchaseOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* PurchaseInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
* ReturnOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* ReturnInvoice: The document is a permanent sales return invoice; document and tax calculation results are saved in the tax history GetTaxResult will return with a DocStatus of Saved.

**ExchangeRate:** decimal, *optional*

Exchange Rate indicates the currency exchange rate from the transaction currency (indicated by CurrencyCode) to the company's base currency. 
Note: ExchangeRate need only be set if the transaction currency is different that of the company's base currency. Default is 1.0

**ExchangeRateEffDate:** date, *optional*

ExchangeRateEffDate indicates the effective date of the exchange rate and works in tandem with ExchangeRate. 
Default is the DocDate if null.

**ExemptionNo:** string [25], *optional*

Exemption or certificate number for the client customer. 
Note: Any value set in this property will cause the document or line to be exempted from tax calculation.

**Lines:** ArrayOfLine, *required*

Document line array. There is a limit of 1000 lines per document, but there must be at least one.

**LocationCode:** string [50], *required if outlet-based reporting is needed, otherwise optional*

Also referred to as a Store Location, Outlet Id, or Outlet code. 
Location code is a value assigned by some State jurisdictions that identifies a particular store location. 
These States may require tax liabilities to be broken out separately for each store Location

**OriginAddress:** Address, *optional*

The Address that will be used as the origin or "Shipped From" location in the tax calculation. 
If no origin address exists at the document level, the destination address will be used in the calculation. 
Note: if no Origin address is provided at the line level, the Document level origin address will be applied here as well. 

**PaymentDate:** date, *optional*

PaymentDate indicates the date that a payment was received for the document. It is only applicable for cash-basis accounting and does not need to be set. The default value is 1900-01-01 which indicates no payment received.

**PurchaseOrderNo:** string [50], *optional*

Purchase Order Number used to create the current document

**ReferenceCode:** string [50], *optional*

Essentially a data field to record the original DocCode of an document if the current document is a ReturnInvoice Document Type

**SalespersonCode:** string [25], *optional*

The client application's salesperson reference code. May also be used to identify a cash register.

**ServiceMode:** enum as string [see below], *optional*

AvaTaxLocal function - provides the ability to control whether a tax is calculated locally or AvaTax web service. The default is Automatic which calculates locally unless a remote connection is necessary for "send sales" not configured at the local server level.

* Automatic
* Local
* Remote

**TaxOverride:** TaxOverride, *optional*

TaxOverride for the document - can be used to manually override components of the tax calculation. See TaxOverride for more information.

### Line

Input property of the GetTaxRequest describing item lines.

#### Properties

**No:** string [50], *required*

Uniquely identifies the line item row.

**OriginCode** string [int MAX_VALUE], *at least one of OriginCode or DestinationCode must be declared either here or at document-level*

The line-level code that refers to the origin address. Line-level address codes will take precedence over document-level address codes if both are present.

**DestinationCode** string [int MAX_VALUE], *at least one of OriginCode or DestinationCode must be declared either here or at document-level*

The line-level code that refers to the destination address. Line-level address codes will take precedence over document-level address codes if both are present.

**ItemCode** string [50], *optional*

Your item identifier, SKU, or UPC.

**TaxCode** string [25], *optional*

AvaTax system tax code or custom tax code

**CustomerUsageType** string [25], *optional*

Same as document-level CustomerUsageType. See code options above in the GetTaxRequest elements.

**ExemptionNo:** string [25], *optional*

Exemption or certificate number for the client customer. 
Note: Any value set in this property will cause the document or line to be exempted from tax calculation.

**Description** string [255], *optional, unless you are bound by Streamlined Sales Tax requirements*

Item description

**Qty** decimal, *optional*

Item quantity. The tax engine does NOT use this as a multiplier with price to get the Amount.

**Amount** decimal, *required*

Total amount of item line (extended amount, qty * unit price)

**Discounted** boolean, *optional*

True if the document level discount is applied to this line item

**TaxIncluded** boolean, *optional*

True if the tax is already included.

**Ref1** string [250], *optional*

Text reference. Use as needed.

**Ref2** string [250], *optional*

Text reference. Use as needed.

**TaxOverride** TaxOverride, *optional*

Same as document-level TaxOverride. Use this if you only need to override individual lines.

### Address

Input property of GetTaxRequest representing addresses needed for tax calculations.

#### Properties

**AddressCode:** string [int MAX_VALUE], *required*

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

### GetTax Result

Document-level tax calculation information.

#### Properties

**DocCode:** string [50]

The document code, if not supplied in the request the returned value is a GUID.

**DocDate:** date

Date of invoice, sales order, purchase order, etc.

**DocStatus:** enum as string [see below]

The document's status after the tax calculation. One of:

* Temporary: GetTaxRequest, DocType = SalesOrder
* Saved: GetTaxRequest, DocType = SalesInvoice
* Posted: PostTaxRequest, Commit = false
* Committed: PostTaxRequest, Commit = true or CommitTaxRequest on document in Posted state
* Cancelled: CancelTaxRequest, CancelCode = DocVoided
* Adjusted: AdjustTaxRequest

**DocType:** DocumentType

The DocumentType used in the GetTaxRequest

**Locked:** boolean

Flag indicating if a Document has been locked by Avalara's Managed Returns Service process. Locked documents can not be modified and can not be cancelled because they have been reported on Tax Return.

**TaxDate:** DateTime

Tax Date is the date used to calculate tax on the Document.

**TaxLines:** TaxLine[]

Tax broken down by individual TaxLine.

**TaxSummary:** TaxDetail[]

Summary of the jurisdiction details for all item lines (returned for detail levels Summary and Line).

**Timestamp:** DateTime

Server timestamp of the request.

**TotalAmount:** decimal

Sum of all line Amount values.

**TotalDiscount:** decimal

Sum of all TaxLine discount amounts.

**TotalTax:** decimal

Sum of all TaxLine tax amounts.

**TotalTaxable:** decimal

Total taxable amount.

**TotalTaxCalculated:** decimal

TotalTaxCalculated indicates the total tax calculated by AvaTax. This is usually the same as the TotalTax, except when a tax override amount is specified. This is for informational purposes. The TotalTax will still be used for reporting.

**TransactionId:** bigint as string

A unique Transaction ID identifying a specific request/response set.

**Version:** int

Current version of the document.

**VolatileTaxRated:** boolean

Deprecated.

**TaxAddresses:** TaxAddress[]

Array of resolved addresses used in the tax calculation.

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

### TaxLine

Taxes for a specific document Line.

#### Properties

**AccountingMethod:** AccountingMethod

This is the accounting applied to the line. Since only Accrual accounting is currently supported, it is always Accrual.

**BoundaryLevel:** BoundaryLevel

The level of jurisdiction boundary precision used for the tax calculation.

**Discount:** decimal

Discount amount applied to this line

**ExemptCertId:** int

Applied ExemptionCertificateId for the Line.

**No:** string [50]

Line Number

**Tax:** decimal

The tax amount, either the calculated amount or an override amount

**Taxability:** boolean

Is the item taxable?

**TaxCalculated:** decimal

TaxCalculated indicates the tax calculated by AvaTax. This will normally be the same as the Tax property unless it has been overridden by a TaxAmount.

**TaxCode:** string [25]

System Tax Code

**TaxDetails:** TaxDetail[]

Tax by jurisdiction. See TaxDetail properties below.

**TaxIncluded:** boolean

Indicates the value of TaxIncluded sent on the line of the GetTaxRequest.

### TaxDetail

Tax details by jurisdiction. Information returned is dependent on the DetailLevel passed in the request.

#### Properties

**Country:** string [2]

2-character ISO country code

**Exemption:** decimal

The portion of the detail that is exempt from taxes.

**JurisCode:** string [10]

Jurisdiction Code for the taxing jurisdiction

**JurisName:** string [200]

Gets the jurisdiction name.

**JurisType:** JurisdictionType

Jurisdiction Type

**NonTaxable:** decimal

The portion of the detail that is not subject to taxes.

**Rate:** decimal

The tax rate for the jurisdiction.

**RateType:** string [1]

RateType indicates the tax rate type. These currently include: 

* F = Food (US)
* G = General (US)
* S = Standard (VAT)
* R = Reduced (VAT)
* Q = Super Reduced (VAT)
* A = Reduced Rate 1 (VAT)
* B = Reduced Rate 2 (VAT)
* Z = Zero Rate

**Region:** string [3]

State or province code

**StateAssignedNo:** string [50]

StateAssignedNo is the identifier given to the jurisdiction by the state. Not all states have these.

**Tax:** decimal

The tax amount, either the calculated amount or an override amount

**Taxable:** decimal

The amount of the sale that is determined to be taxable.

**TaxAuthorityType:** int

Internal tax authority type identifier used by our returns engine.

**TaxCalculated:** decimal

TaxCalculated indicates the tax calculated by AvaTax. It will usually be the same as the Tax property, unless it has been overridden by a TaxAmount.

**TaxName:** string [75]

It further defines the tax and jurisdiction.

**TaxType:** TaxType

Tax Type - Sales or Seller's Use

### TaxAddress

TaxAddress represents canonical addresses used in tax calculation.

#### Properties

**Address:** string [50]

Canonical street address

**AddressCode:** string

Reference code uniquely identifying this address instance. AddressCode will always correspond to an address code supplied to in the address collection provided in the request.

**City:** string [50]

City name

**Region:** string [3]

State or region name

**Country:** string

Country code, as ISO 3166-1 (Alpha-2) country code (e.g. “US”)

**PostalCode:** string

Postal code

**Latitude:** decimal

Geographic latitude. Latitude is only defined if input address was a geographic point.

**Longitude:** decimal

Geographic longitude. Longitude is only defined if input address was a geographic point.

**TaxRegionId:** string

AvaTax tax region identifier

**JurisCode:** string

Tax jurisdiction code