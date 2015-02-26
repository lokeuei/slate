## AdjustTax

```shell
TBD
```

```csharp
TaxSvc taxSvc = new TaxSvc();

taxSvc.Configuration.Security.Account ="1234567890";
taxSvc.Configuration.Security.License = "A1B2C3D4E5F6G7H8";
taxSvc.Configuration.Url = "https://development.avalara.net";
taxSvc.Configuration.ViaUrl = "https://development.avalara.net";
taxSvc.Profile.Client = "AvaTaxSample";
taxSvc.Profile.Name = "Development";

AdjustTaxRequest adjustTaxRequest = new AdjustTaxRequest();

adjustTaxRequest.AdjustmentReason = 4;
adjustTaxRequest.AdjustmentDescription = "Transaction Adjusted for Testing";

GetTaxRequest getTaxRequest = new GetTaxRequest();

getTaxRequest.CustomerCode = "ABC4335";
getTaxRequest.DocDate = DateTime.Parse("2014-01-01");
getTaxRequest.CompanyCode = "APITrialCompany";
getTaxRequest.DocCode = "INV001";
getTaxRequest.DetailLevel = DetailLevel.Tax;
getTaxRequest.Commit = false;
getTaxRequest.DocType = DocumentType.SalesInvoice;
// getTaxRequest.BusinessIdentificationNo="234243";
// getTaxRequest.CustomerUsageType = "G";
// getTaxRequest.ExemptionNo = "12345";
// getTaxRequest.Discount = 50;
// getTaxRequest.LocationCode = "01";
// getTaxRequest.TaxOverride.TaxOverrideType = TaxOverrideType.TaxDate;
// getTaxRequest.TaxOverride.Reason = "Adjustment for return";
// getTaxRequest.TaxOverride.TaxDate = DateTime.Parse("2013-07-01");
// getTaxRequest.TaxOverride.TaxAmount=0 ;
// getTaxRequest.ServiceMode = ServiceMode.Automatic;
getTaxRequest.PurchaseOrderNo = "PO123456";
getTaxRequest.ReferenceCode = "ref123456";
getTaxRequest.PosLaneCode = "09";
getTaxRequest.CurrencyCode = "USD";
getTaxRequest.ExchangeRate = (decimal)1.0;
getTaxRequest.ExchangeRateEffDate = DateTime.Parse("2013-01-01");
getTaxRequest.SalespersonCode = "Bill Sales";

Address address1 = new Address();
address1.Line1 = "45 Fremont Street";
address1.City = "San Francisco";
address1.Region = "CA";

Address address2 = new Address();
address2.Line1 = "118 N Clark St";
address2.Line2 = "Suite 100";
address2.Line3 = "ATTN Accounts Payable";
address2.City = "Chicago";
address2.Region = "IL";
address2.Country = "US";
address2.PostalCode = "60602";

Address address3 = new Address();
address3.Latitude = "47.627935";
address3.Longitude = "-122.51702";

getTaxRequest.OriginAddress = address1;
getTaxRequest.DestinationAddress = address2;

Line line1 = new Line();
line1.No = "01";
line1.ItemCode = "N543";
line1.Qty = 1;
line1.Amount = 10;
line1.OriginAddress = address1;
line1.DestinationAddress = address2;
line1.Description = "Red Size 7 Widget";
line1.TaxCode = "NT";
// line1.CustomerUsageType = "L";
// line1.ExemptionNo = "12345";
// line1.Discounted = true;
// line1.TaxIncluded = true;
// line1.TaxOverride.TaxOverrideType = TaxOverrideType.TaxDate;
// line1.TaxOverride.Reason = "Adjustment for return";
// line1.TaxOverride.TaxDate = DateTime.Parse("2013-07-01");
// line1.TaxOverride.TaxAmount = 0;
line1.Ref1 = "ref123";
line1.Ref2 = "ref456";
getTaxRequest.Lines.Add(line1);

Line line2 = new Line();
line2.No = "02";
line2.ItemCode = "T345";
line2.Qty = 3;
line2.Amount = 150;
line2.OriginAddress = address1;
line2.DestinationAddress = address3;
line2.Description = "Size 10 Green Running Shoe";
line2.TaxCode = "PC030147";
getTaxRequest.Lines.Add(line2);

Line line3 = new Line();
line3.No = "02-FR";
line3.ItemCode = "FREIGHT";
line3.Qty = 1;
line3.Amount = 15;
line3.OriginAddress = address1;
line3.DestinationAddress = address3;
line3.Description = "Shipping Charge";
line3.TaxCode = "FR";
getTaxRequest.Lines.Add(line3);

adjustTaxRequest.GetTaxRequest = getTaxRequest;
AdjustTaxResult adjustTaxResult = taxSvc.AdjustTax(adjustTaxRequest);

```

```php
<?php
require('../../AvaTax4PHP/AvaTax.php');

new ATConfig('Development', array(
    'url' => 'https://development.avalara.net',
    'account' => '1234567890',
    'license' => 'A1B2C3D4E5F6G7H8')
);

$taxSvc = new TaxServiceSoap('Development');

$adjustTaxRequest = new AdjustTaxRequest();
$adjustTaxRequest->setAdjustmentReason(4);
$adjustTaxRequest->setAdjustmentDescription("Transaction Adjusted for Testing");

$getTaxRequest = new GetTaxRequest();

$getTaxRequest->setCompanyCode("APITrialCompany");
$getTaxRequest->setDocType("SalesInvoice");
$getTaxRequest->setDocCode("INV001");
$getTaxRequest->setDocDate("2014-01-01");
$getTaxRequest->setCustomerCode("ABC4335");
$getTaxRequest->setDetailLevel(DetailLevel::$Tax);
//$getTaxRequest->setSalespersonCode("Bill Sales");
//$getTaxRequest->setCustomerUsageType("G");
//$getTaxRequest->setDiscount(5.00);
//$getTaxRequest->setPurchaseOrderNo("PO123456");
//$getTaxRequest->setExemptionNo("12345");
//$getTaxRequest->setReferenceCode("ref123456");
//$getTaxRequest->setLocationCode("01");
//$getTaxRequest->setCommit(false);
//$getTaxRequest->setDiscount(5.00);
//$getTaxRequest->setCurrencyCode("USD");
//$getTaxRequest->setServiceMode("Automatic");
//$getTaxRequest->setExchangeRate("1.0");
//$getTaxRequest->setExchangeRateEffDate("2013-01-01");
//$getTaxRequest->setPosLaneCode("09");
//$getTaxRequest->setBusinessIdentificationNo(234243);
//$taxOverride = new TaxOverride();
//$getTaxRequest->setTaxOverride($taxOverride); 
//$taxOverride->setTaxOverrideType(TaxOverrideType::$TaxDate);
//$taxOverride->setTaxAmount(0.00);
//$taxOverride->setReason("Adjustment for return");
//$taxOverride->setTaxDate("2013-07-01");

$line1 = new Line();
$line1->setNo(1);
$line1->setItemCode("N543");
$line1->setDescription("Red Size 7 Widget");
$line1->setQty(1);
$line1->setAmount(10);
$line1->setTaxCode("NT");
//$line1->setDiscounted(true);
//$line->setTaxIncluded(true);
//$line1->setRevAcct("");
//$line1->setRef1("ref123");
//$line1->setRef2("ref456");
//$line1->setExemptionNo("12345");
//$line1->setCustomerUsageType("L");
//$taxOverride = new TaxOverride();
//$line1->setTaxOverride($taxOverride);
//$taxOverride->setTaxOverrideType(TaxOverrideType::$TaxDate);
//$taxOverride->setTaxAmount(0.00);
//$taxOverride->setReason("Adjustment for return");
//$taxOverride->setTaxDate("2013-07-01");

$line2 = new Line();
$line2->setNo(2);
$line2->setOriginAddress($OrigAddress);
$line2->setDestinationAddress($thirdaddress);
$line2->setItemCode("T345");
$line2->setDescription("Size 10 Green Running Shoe");
$line2->setQty(3);
$line2->setAmount(150);
$line2->setTaxCode("PC030147");

$line3 = new Line();
$line3->setOriginAddress($OrigAddress);
$line3->setDestinationAddress($thirdaddress);
$line3->setNo(3);
$line3->setItemCode("FREIGHT");
$line3->setDescription("Shipping Charge");
$line3->setQty(1);
$line3->setAmount(15);
$line3->setTaxCode("FR");

$getTaxRequest->setLines(array($line1, $line2, $line3));

$origin = new Address();
$origin->setLine1("45 Fremont Street");
$origin->setCity("San Francisco");
$origin->setRegion("CA");
$origin->setCountry("US");
$getTaxRequest->setOriginAddress($origin);

$destination = new Address();
$destination->setLine1("118 N Clark St");
$destination->setLine2("Suite 100");
$destination->setLine3("ATTN Accounts Payable");
$destination->setCity("Chicago");
$destination->setRegion("IL");
$destination->setPostalCode("60602-1304");
$destination->setCountry("US");
$getTaxRequest->setDestinationAddress($destination);

$thirdaddress = new Address();
$thirdaddress->setLine1("100 Ravine Lane");
$thirdaddress->setLine2("Suite 100");
$thirdaddress->setLine3("");
$thirdaddress->setCity("Bainbridge Island");
$thirdaddress->setRegion("WA");
$thirdaddress->setPostalCode("98110");
$thirdaddress->setCountry("US");
$getTaxRequest->setAddressCode($thirdaddress);

$adjustTaxRequest->setGetTaxRequest($getTaxRequest);
$adjustTaxResult = $taxSvc->AdjustTax($adjustTaxRequest);
?>

```

```java
TaxSvcLocator taxSvcLocator = new TaxSvcLocator();
String url = "https://development.avalara.net";
TaxSvcSoap taxSvc = taxSvcLocator.getTaxSvcSoap(new URL(url));
Profile profile = new Profile();
profile.setClient("AvaTaxSample");
taxSvc.setProfile(profile);
Security security = new Security();
security.setAccount("1234567890");
security.setLicense("A1B2C3D4E5F6G7H8");
taxSvc.setSecurity(security);

AdjustTaxRequest adjustTaxRequest = new AdjustTaxRequest();
adjustTaxRequest.setAdjustmentDescription("Transaction Adjusted for Testing");
adjustTaxRequest.setAdjustmentReason(4);

GetTaxRequest getTaxRequest = new GetTaxRequest();
Format formatter = new SimpleDateFormat("yyyy-MM-dd");

getTaxRequest.setCompanyCode("APITrialCompany");
getTaxRequest.setDocType(DocumentType.SalesInvoice);
getTaxRequest.setDocCode("INV001");
Date docDate = (Date)formatter.parseObject("2014-01-01");
getTaxRequest.setDocDate(docDate);
getTaxRequest.setCustomerCode("ABC4335");
getTaxRequest.setDetailLevel(DetailLevel.Tax);
getTaxRequest.setOriginCode("01");
getTaxRequest.setDestinationCode("02");

// getTaxRequest.setSalespersonCode("Bill Sales");
// getTaxRequest.setCustomerUsageType("G");
// getTaxRequest.setDiscount(new BigDecimal(50.00));
// getTaxRequest.setPurchaseOrderNo("PO123456");
// getTaxRequest.setExemptionNo("12345");
// getTaxRequest.setReferenceCode("ref123456");
// getTaxRequest.setLocationCode("01");
// getTaxRequest.setCommit(true);
// getTaxRequest.setCurrencyCode("USD");
// getTaxRequest.setServiceMode(ServiceMode.Automatic);
// getTaxRequest.setExchangeRate(new BigDecimal(9.00));
// Date ExchangeRateEffDate = (Date)formatter.parseObject("2013-01-01");
// getTaxRequest.setExchangeRateEffDate(ExchangeRateEffDate);
// getTaxRequest.setPosLaneCode("09");
// getTaxRequest.setBusinessIdentificationNo("234243");
//  
// TaxOverride taxOverride = new TaxOverride();
// taxOverride.setReason("Adjustment for return");
// taxOverride.setTaxOverrideType(TaxOverrideType.TaxDate);
// taxOverride.setTaxAmount(new BigDecimal(0.00));
// Date taxOverrideDate = (Date)formatter.parseObject("2013-07-01");
// taxOverride.setTaxDate(taxOverrideDate);
// getTaxRequest.setTaxOverride(taxOverride);

ArrayOfLine lines = new ArrayOfLine(3);
Line line;

line = new Line();
line.setNo("01");
line.setItemCode("N543");
line.setDescription("Red Size 7 Widget");
line.setTaxCode("PC030147");
line.setQty(new BigDecimal(1.00));
line.setAmount(new BigDecimal(10.00));
line.setTaxCode("NT");

//    line.setCustomerUsageType("L");
//    line.setExemptionNo("12345");
//    line.setDiscounted(true);
//    line.setTaxIncluded(true);
//    line.setRef1("123");
//    line.setRef2("456");

lines.add(line);

line = new Line();
line.setNo("02");
line.setOriginCode("01");
line.setDestinationCode("03");
line.setItemCode("T345");
line.setDescription("Size 10 Green Running Shoe");
line.setQty(new BigDecimal(3.00));
line.setAmount(new BigDecimal(150.00));
line.setTaxCode("PC030147");
lines.add(line);

line = new Line();
line.setOriginCode("01");
line.setDestinationCode("03");
line.setNo("03");
line.setItemCode("FREIGHT");
line.setDescription("Shipping Charge");
line.setQty(new BigDecimal(1.00));
line.setAmount(new BigDecimal(15.00));
line.setTaxCode("FR");
lines.add(line);

getTaxRequest.setLines(lines);

ArrayOfBaseAddress addresses = new ArrayOfBaseAddress(3);

BaseAddress address1 = new BaseAddress();
address1.setAddressCode("01");
address1.setLine1("45 Fremont Street");
address1.setLine2("");
address1.setLine3("");
address1.setCity("San Francisco");
address1.setRegion("CA");
address1.setPostalCode("94105");
address1.setCountry("US");
addresses.add(address1);

BaseAddress address2 = new BaseAddress();
address2.setAddressCode("02");
address2.setLine3("ATTN Accounts Payable");
address2.setLine1("118 N Clark St");
address2.setLine2("Suite 100");
address2.setCity("Chicago");
address2.setRegion("IL");
address2.setPostalCode("60602");
address2.setCountry("US");
addresses.add(address2);

BaseAddress address3 = new BaseAddress();
address3.setAddressCode("03");
address3.setLatitude("47.627935");
address3.setLongitude("-122.51702");
addresses.add(address3);

getTaxRequest.setAddresses(addresses);

adjustTaxRequest.setGetTaxRequest(getTaxRequest);

AdjustTaxResult adjustTaxResult = taxSvc.adjustTax(adjustTaxRequest);
```

> The above command returns XML structured like this:

```xml
<AdjustTaxResult>
<TransactionId>0</TransactionId>
<ResultCode>Success</ResultCode>
<DocId>48769272</DocId>
<DocType>SalesInvoice</DocType>
<DocCode>INV001</DocCode>
<DocDate>2014-01-01</DocDate>
<DocStatus>Saved</DocStatus>
<Reconciled>false</Reconciled>
<Timestamp>2014-03-25T23:20:34.9880568Z</Timestamp>
<TotalAmount>175</TotalAmount>
<TotalDiscount>0</TotalDiscount>
<TotalExemption>10.94</TotalExemption>
<TotalTaxable>164.06</TotalTaxable>
<TotalTax>14.27</TotalTax>
<TotalTaxCalculated>14.27</TotalTaxCalculated>
<HashCode>0</HashCode>
<TaxLines>
<TaxLine>
<No>01</No>
<TaxCode>NT</TaxCode>
<Taxability>false</Taxability>
<BoundaryLevel>Address</BoundaryLevel>
<Exemption>10</Exemption>
<Discount>0</Discount>
<Taxable>0</Taxable>
<Rate>0.092500</Rate>
<Tax>0</Tax>
<TaxCalculated>0</TaxCalculated>
<TaxIncluded>false</TaxIncluded>
<TaxDetails>
<TaxDetail>
<Country>US</Country>
<Region>IL</Region>
<JurisType>State</JurisType>
<JurisCode>17</JurisCode>
<TaxType>Sales</TaxType>
<Base>0</Base>
<Taxable>0</Taxable>
<Rate>0.062500</Rate>
<Tax>0</Tax>
<TaxCalculated>0</TaxCalculated>
<NonTaxable>10</NonTaxable>
<Exemption>0</Exemption>
<JurisName>ILLINOIS</JurisName>
<TaxName>IL STATE TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
</TaxDetail>
<TaxDetail>
<Country>US</Country>
<Region>IL</Region>
<JurisType>County</JurisType>
<JurisCode>031</JurisCode>
<TaxType>Sales</TaxType>
<Base>0</Base>
<Taxable>0</Taxable>
<Rate>0.007500</Rate>
<Tax>0</Tax>
<TaxCalculated>0</TaxCalculated>
<NonTaxable>10</NonTaxable>
<Exemption>0</Exemption>
<JurisName>COOK</JurisName>
<TaxName>IL COUNTY TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
</TaxDetail>
<TaxDetail>
<Country>US</Country>
<Region>IL</Region>
<JurisType>City</JurisType>
<JurisCode>14000</JurisCode>
<TaxType>Sales</TaxType>
<Base>0</Base>
<Taxable>0</Taxable>
<Rate>0.012500</Rate>
<Tax>0</Tax>
<TaxCalculated>0</TaxCalculated>
<NonTaxable>10</NonTaxable>
<Exemption>0</Exemption>
<JurisName>CHICAGO</JurisName>
<TaxName>IL CITY TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
</TaxDetail>
<TaxDetail>
<Country>US</Country>
<Region>IL</Region>
<JurisType>Special</JurisType>
<JurisCode>AQOF</JurisCode>
<TaxType>Sales</TaxType>
<Base>0</Base>
<Taxable>0</Taxable>
<Rate>0.010000</Rate>
<Tax>0</Tax>
<TaxCalculated>0</TaxCalculated>
<NonTaxable>10</NonTaxable>
<Exemption>0</Exemption>
<JurisName>REGIONAL TRANSPORT. 
AUTHORITY (RTA)</JurisName>
<TaxName>IL SPECIAL TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
</TaxDetail>
</TaxDetails>
<ExemptCertId>0</ExemptCertId>
<TaxDate>2014-01-01</TaxDate>
<ReportingDate>2014-01-01</ReportingDate>
<AccountingMethod>Accrual</AccountingMethod>
</TaxLine>
<TaxLine>
<No>02</No>
<TaxCode>PC030147</TaxCode>
<Taxability>true</Taxability>
<BoundaryLevel>Zip5</BoundaryLevel>
<Exemption>0</Exemption>
<Discount>0</Discount>
<Taxable>150</Taxable>
<Rate>0.087000</Rate>
<Tax>13.05</Tax>
<TaxCalculated>13.05</TaxCalculated>
<TaxIncluded>false</TaxIncluded>
<TaxDetails>
<TaxDetail>
<Country>US</Country>
<Region>WA</Region>
<JurisType>State</JurisType>
<JurisCode>53</JurisCode>
<TaxType>Sales</TaxType>
<Base>150</Base>
<Taxable>150</Taxable>
<Rate>0.065000</Rate>
<Tax>9.75</Tax>
<TaxCalculated>9.75</TaxCalculated>
<NonTaxable>0</NonTaxable>
<Exemption>0</Exemption>
<JurisName>WASHINGTON</JurisName>
<TaxName>WA STATE TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo/>
</TaxDetail>
<TaxDetail>
<Country>US</Country>
<Region>WA</Region>
<JurisType>City</JurisType>
<JurisCode>03736</JurisCode>
<TaxType>Sales</TaxType>
<Base>150</Base>
<Taxable>150</Taxable>
<Rate>0.022000</Rate>
<Tax>3.3</Tax>
<TaxCalculated>3.3</TaxCalculated>
<NonTaxable>0</NonTaxable>
<Exemption>0</Exemption>
<JurisName>BAINBRIDGE ISLAND</JurisName>
<TaxName>WA CITY TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>1804</StateAssignedNo>
</TaxDetail>
</TaxDetails>
<ExemptCertId>0</ExemptCertId>
<TaxDate>2014-01-01</TaxDate>
<ReportingDate>2014-01-01</ReportingDate>
<AccountingMethod>Accrual</AccountingMethod>
</TaxLine>
<TaxLine>
<No>02-FR</No>
<TaxCode>FR</TaxCode>
<Taxability>true</Taxability>
<BoundaryLevel>Zip5</BoundaryLevel>
<Exemption>0.94</Exemption>
<Discount>0</Discount>
<Taxable>14.06</Taxable>
<Rate>0.087000</Rate>
<Tax>1.22</Tax>
<TaxCalculated>1.22</TaxCalculated>
<TaxIncluded>false</TaxIncluded>
<TaxDetails>
<TaxDetail>
<Country>US</Country>
<Region>WA</Region>
<JurisType>State</JurisType>
<JurisCode>53</JurisCode>
<TaxType>Sales</TaxType>
<Base>14.06</Base>
<Taxable>14.06</Taxable>
<Rate>0.065000</Rate>
<Tax>0.91</Tax>
<TaxCalculated>0.91</TaxCalculated>
<NonTaxable>0.94</NonTaxable>
<Exemption>0</Exemption>
<JurisName>WASHINGTON</JurisName>
<TaxName>WA STATE TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo/>
</TaxDetail>
<TaxDetail>
<Country>US</Country>
<Region>WA</Region>
<JurisType>City</JurisType>
<JurisCode>03736</JurisCode>
<TaxType>Sales</TaxType>
<Base>14.06</Base>
<Taxable>14.06</Taxable>
<Rate>0.022000</Rate>
<Tax>0.31</Tax>
<TaxCalculated>0.31</TaxCalculated>
<NonTaxable>0.94</NonTaxable>
<Exemption>0</Exemption>
<JurisName>BAINBRIDGE ISLAND</JurisName>
<TaxName>WA CITY TAX</TaxName>
<TaxAuthorityType>45</TaxAuthorityType>
<TaxGroup/>
<RateType>G</RateType>
<StateAssignedNo>1804</StateAssignedNo>
</TaxDetail>
</TaxDetails>
<ExemptCertId>0</ExemptCertId>
<TaxDate>2014-01-01</TaxDate>
<ReportingDate>2014-01-01</ReportingDate>
<AccountingMethod>Accrual</AccountingMethod>
</TaxLine>
</TaxLines>
<TaxAddresses>
<TaxAddress>
<Address>45 Fremont St</Address>
<AddressCode>12337243</AddressCode>
<BoundaryLevel>0</BoundaryLevel>
<City>San Francisco</City>
<Country>US</Country>
<PostalCode>94105-2204</PostalCode>
<Region>CA</Region>
<TaxRegionId>2113460</TaxRegionId>
<JurisCode/>
<Latitude>37.791119</Latitude>
<Longitude>-122.397366</Longitude>
<GeocodeType>StreetLevel</GeocodeType>
<ValidateStatus>NormalHit</ValidateStatus>
<DistanceToBoundary>0</DistanceToBoundary>
</TaxAddress>
<TaxAddress>
<Address>45 Fremont St</Address>
<AddressCode>12337243</AddressCode>
<BoundaryLevel>0</BoundaryLevel>
<City>San Francisco</City>
<Country>US</Country>
<PostalCode>94105-2204</PostalCode>
<Region>CA</Region>
<TaxRegionId>2113460</TaxRegionId>
<JurisCode/>
<Latitude>37.791119</Latitude>
<Longitude>-122.397366</Longitude>
<GeocodeType>StreetLevel</GeocodeType>
<ValidateStatus>NormalHit</ValidateStatus>
<DistanceToBoundary>0</DistanceToBoundary>
</TaxAddress>
<TaxAddress>
<Address>45 Fremont St</Address>
<AddressCode>12337243</AddressCode>
<BoundaryLevel>0</BoundaryLevel>
<City>San Francisco</City>
<Country>US</Country>
<PostalCode>94105-2204</PostalCode>
<Region>CA</Region>
<TaxRegionId>2113460</TaxRegionId>
<JurisCode>0607500000</JurisCode>
<Latitude>37.791119</Latitude>
<Longitude>-122.397366</Longitude>
<GeocodeType>StreetLevel</GeocodeType>
<ValidateStatus>NormalHit</ValidateStatus>
<DistanceToBoundary>0</DistanceToBoundary>
</TaxAddress>
<TaxAddress>
<Address>118 N Clark St Ste 100</Address>
<AddressCode>18305036</AddressCode>
<BoundaryLevel>0</BoundaryLevel>
<City>Chicago</City>
<Country>US</Country>
<PostalCode>60602-1304</PostalCode>
<Region>IL</Region>
<TaxRegionId>2062953</TaxRegionId>
<JurisCode>1703114000</JurisCode>
<Latitude>41.884132</Latitude>
<Longitude>-87.631048</Longitude>
<GeocodeType>StreetLevel</GeocodeType>
<ValidateStatus>NormalHit</ValidateStatus>
<DistanceToBoundary>0</DistanceToBoundary>
</TaxAddress>
<TaxAddress>
<Address/>
<AddressCode>18420268</AddressCode>
<BoundaryLevel>2</BoundaryLevel>
<City/>
<Country>US</Country>
<PostalCode/>
<Region>WA</Region>
<TaxRegionId>2109716</TaxRegionId>
<JurisCode/>
<Latitude>47.627935</Latitude>
<Longitude>-122.51702</Longitude>
<GeocodeType/>
<ValidateStatus>Not Validated</ValidateStatus>
<DistanceToBoundary>2392</DistanceToBoundary>
</TaxAddress>
<TaxAddress>
<Address/>
<AddressCode>18420268</AddressCode>
<BoundaryLevel>2</BoundaryLevel>
<City/>
<Country>US</Country>
<PostalCode/>
<Region>WA</Region>
<TaxRegionId>2109716</TaxRegionId>
<JurisCode>5303503736</JurisCode>
<Latitude>47.627935</Latitude>
<Longitude>-122.51702</Longitude>
<GeocodeType/>
<ValidateStatus>Not Validated</ValidateStatus>
<DistanceToBoundary>2392</DistanceToBoundary>
</TaxAddress>
</TaxAddresses>
<Locked>false</Locked>
<AdjustmentReason>4</AdjustmentReason>
<AdjustmentDescription>
Transaction Adjusted for Testing</AdjustmentDescription>
<Version>2</Version>
<TaxDate>2014-01-01</TaxDate>
<TaxSummary/>
<VolatileTaxRates>false</VolatileTaxRates>
</AdjustTaxResult>

```

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