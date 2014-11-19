## IsAuthorized

IsAuthorized allows you to send a user's credentials along with a list of AvaTax methods to check which methods that user is authorized to use. You can also get your account expiration date via this method. There is technically no request to build - just a string to pass in the method call when you instantiate the result object.

### IsAuthorized Result

Result data returned from IsAuthorized.

#### Properties

**Expires:** DateTime

The date and time at which your AvaTax account will expire.

**Operations:** string [255]

The operations that the current user is authorized to use. Determined from the list provided in the IsAuthorized call.

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
