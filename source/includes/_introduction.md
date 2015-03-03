# Introduction

The Avalara AvaTax Excise Web Service is a SOAP web service that is the external programmatic interface into the Avalara AvaTax Excise application.   It provides for a platform independent mechanism to obtain tax calculation information.  This document defines the object structure, and an introduction on how to consume the web service for use in customer programs.

Please note the application name changes effective 7/31/2014:
•	Avalara Returns Excise replaces Zytax Compliance
•	Avalara AvaTax Excise replaces Zytax Determination
•	Avalara Government replaces Zytax Government

URLs
Development Authentication Service: https://psd.avalara.net/authenticationservice.asmx?wsdl
Development Tax Determination:  https://psd.avalara.net/determination/taxdetermination.asmx?wsdl
User Acceptance Authentication Service: https://exciseua.avalara.net/authenticationservice.asmx?wsdl
User Acceptance Tax Determination: https://exciseua.avalara.net/determination/taxdetermination.asmx?wsdl
Production Authentication Service: https://excise.avalara.net/authenticationservice.asmx?wsdl
Production Tax Determination: https://excise.avalara.net/determination/taxdetermination.asmx?wsdl
