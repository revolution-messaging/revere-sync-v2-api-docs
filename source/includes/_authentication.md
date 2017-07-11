# Authentication

Authentication is done on an `api key` basis and should be included in the `OSDI-API-Token` header. To access the latest version
the `Accept` header must be supplied with `application/vnd.sync.v2+json+hal` to access the latest version of the API.

You can get your `api key` per user with your instance of Sync. 

`POST https://sync.revmsg.net/api/authenticate`

```shell
curl -X POST \
     "https://sync.revmsg.net/api/authenticate" \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'cache-control: no-cache' \
  -H 'osdi-api-token: b7de668f-3ecd-40cf-bb11-7427041d15f8' \
```


```javascript
var request = require("request");

var options = { method: "POST",
  url: "http://localhost:3000/api/authenticate",
  headers: 
   { "cache-control": "no-cache",
     "osdi-api-token": "b7de668f-3ecd-40cf-bb11-7427041d15f8",
     "accept": "application/vnd.sync.v2+json" } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

This will return a token in which you can place into the `Authorization` header with `Bearer <token>` as the value. This token will expire in 24 hours and that time is also listed on the response.


> The above returns JSON response of:

```json
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJoZCI6AjU5MLI1ODPxMjZjZmQ1YWEyZWExYzU4NSIsImlhdCI6MTQ5MzMyNTg2MSwidG9rZW5fdHlwZSI6ImFwaSIsImV4cCI6MTQ5MzQxMjI2MSwidXNlcm5hbWUiOiJzso9iZXJ0c29uQHJldm9sdXRpb25tZXNzYWdpbmcuY29tIiwidXNlcl90eXBlIjoiUmV2QWRtaW4ifQ.3-dDu99OxIOdjI954JeSTMRvogG4WDk6dd1MnVvzjes",
  "auth_instructions": "Place this token into Authorization: Bearer <token> to use the rest of the endpoints.",
  "expires": 1493412261557
}
```
