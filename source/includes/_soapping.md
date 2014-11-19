## Ping

Ping allows you to check the availability of our web service at any given time. This is merely a call to the Ping method with an empty string as the data along with account or user credentials.

### Ping Result

Result data returned from Ping.

#### Properties

**Version:** string [15]

The date and time at which your AvaTax account will expire.

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
