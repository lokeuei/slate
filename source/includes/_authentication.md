# Excise Tax Authentication Overview

The Excise Platform Authentication Web Service is a SOAP/XML web service that is the external programmatic interface for authentication against the Excise Platform.   It provides for a platform independent mechanism to obtain an authorization token which can be used when calling other web services.  This document defines the object structure, and an introduction on how to consume the web service for use in customer programs.  

Web service authentication in the Excise platform has 3 basic forms:
* Anonymous – no authentication required to call a web service
* Forms – require a forms authentication cookie to be passed with each web service call
* NTLM – use the built in windows authentication to restrict access to the web service

Forms authentication requires calling the AuthenticationService.asmx before calling other web services.  This function returns an ASP.Net Forms authentication cookie with the response which needs to be passed along with each future web service call.

NTLM authentication does not require calling the AuthenticationService.asmx before calling other web services.  At the beginning of the call to the web service, the user is authenticated, and if successful, the call is processed normally.  The web service will attach a Forms Authentication cookie to the response to improve performance in subsequent calls, but it is not required to use the cookie (the caller can be re-authenticated each time).  The client must keep the TCP connection alive in between calls in order to re-use the cookie while configured to use NTLM.  Each new TCP connection will require re-authentication.
