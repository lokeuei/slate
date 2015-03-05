# Forms Authentication Methods

The Avalara SOAP API exposes all methods available for interacting with the AvaTax service, allowing calculation of tax, modification of documents, and validation of addresses - including some functionality not exposed by our REST API.
If you're unsure of which API to use, a full comparison of the differences between the functionality provided by our REST and SOAP interfaces is documented <a href='http://developer.avalara.com/api-docs/designing-your-integration/soap-or-rest' target="_parent">here</a>.


**URLs**

- Development Authentication Service:  <a href='https://psd.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://psd.avalara.net/authenticationservice.asmx?WSDL </a>
- User Acceptance Authentication Service:  <a href='https://exciseua.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://exciseua.avalara.net/authenticationservice.asmx?WSDL</a>
- Production Authentication Service:  <a href='https://excise.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://excise.avalara.net/authenticationservice.asmx?WSDL</a>

## Login Request
```csharp
public class MainClass 
{
    private static System.Net.CookieContainer _authCookies = null;
    MaintenanceImportService _mi = new MaintenanceImportService();
    
    public static void Main() 
    {
        InvokeLocationsImport();
    }

    private static void Login()
    {
        if (_authCookies != null)
        {
            //Already connected, try to reuse connection.
        }
        else
        {
            AuthenticationService auth = new AuthenticationService();
            auth.CookieContainer = new System.Net.CookieContainer();

            //Connecting...
            if (auth.Login(“username”, “password”, “Determination Oil Company”))
            {
                _authCookies = auth.CookieContainer;
                //Connected.
            }
            else
            {
                _ authCookies = null;
                //failed!
            }
        }
    }

    public static void InvokeLocationsImport()
    {
        Login();

        if (_authCookies != null)
        {
            _mi.CookieContainer = _authCookies;

            List<Location_2_0_031> locations = new List<Location_2_0_031>();

            Location_2_0_031 location = new Location_2_0_031();
            location.Description = "ZZ Oil";
            location.EffectiveDate = new DateTime(2009, 1, 1);
            location.Address1 = "123 Main St.";
            location.Address2 = "Suite B.";
            location.City = "Green Bay";
            location.Jurisdiction = "WI";
            location.CountryCode = "USA";
            location.PostalCode = "54313";
            location.OutsideCityLimitInd = YesNo.No;

            locations.Add(location);

            LocationImportResultSummary_2_0_031 result =
                _mi.ImportLocations(locations.ToArray(), "Determination Oil Company", 100, 100, 100, true);

            Dumper.Dump("result", result);
        }
    }
}
```
``` xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <Login xmlns="http://taxes.services.fuelquest.com/">
      <userName>username</userName>
      <password>password</password>
      <companyName>Determination Oil Company</companyName>
    </Login>
  </soap:Body>
</soap:Envelope>
```

Authenticates the user against the configured membership provider and verifies they have access to the specified company.  If successful, an authentication token is return as a cookie.

**userName:** string, *required*
The user's login

**password:** string, *required*
The user's password

**companyName:** string, *required*
The name of the company to use for the remainder of the session.

## Login Response
``` xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <LoginResponse xmlns="http://taxes.services.fuelquest.com/">
      <LoginResult>true</LoginResult>
    </LoginResponse>
  </soap:Body>
</soap:Envelope>
```
**LoginResult:** boolean

## Logout Request
``` xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <Logout xmlns="http://taxes.services.fuelquest.com/" />
  </soap:Body>
</soap:Envelope>
```

Logs the current user out of the system and clears their authentication cookie.


## Logout Response
``` xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <LogoutResponse xmlns="http://taxes.services.fuelquest.com/" />
  </soap:Body>
</soap:Envelope>
```
