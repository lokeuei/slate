# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: AvalaraApiKey meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Avalara uses API keys to allow access to the API. 
The API key is issued upon registering for an account. 
You can get an API key at our [developer portal](http://getrates-dev.avlr.sh/).

Avalara expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: AvalaraApiKey meowmeowmeow`

<aside class="warning">
You must replace `meowmeowmeow` with your personal API key.
</aside>