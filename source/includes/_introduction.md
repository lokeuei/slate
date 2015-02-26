# Introduction

The Avalara AvaTax APIs allow you to connect your web cart or accounting software to realtime tax calculation and address validation services. You can just retrieve tax amounts, but your transactions can also be recorded for reporting and tax filing. We have a RESTful API, class wrappers (adapters) for PHP, Java, and .NET compiled from the SOAP API, or you can build your own wrappers directly from the [address](https://development.avalara.net/address/addresssvc.wsdl) and [tax service](https://development.avalara.net/tax/taxsvc.wsdl) SOAP WSDLs.

The Avalara AvaTax service is SOAP-based, so that API covers all AvaTax functionality. However, we understand the demand for a more RESTful interface, so we provide an API for that as well for the main functions of the AvaTax service. If you're unsure of which API to use, a full comparison of the differences between the functionality provided by our REST and SOAP interfaces is documented [here](http://developer.avalara.com/api-docs/designing-your-integration/soap-or-rest).

The sample code on this page is intended to give you an idea of how the methods are used, but you can find functioning sample source projects with full class libraries from our <a href='http://github.com/avadev'>API Sample Code page</a>.

<aside> You will not be able to make web service calls until you have received an active account number and license key via email, or a username and password from the <a href='http://developer.avalara.com/getting-started'>get-started sandbox registration</a>. </aside>
