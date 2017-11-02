# Services
**Note: This endpoint is not OSDI enabled.**

## Revere Mobile Services

This is the entry point to retrive Revere Mobile Services and Revere Mobile Flows.

## The Revere Mobile Service Object

Attribute                      | Type     | Description
-----------------------------  | -------- | -----------
id                             | ObjectId | Unique ID for the Mobile Service.
name                           | string   | Name for the Mobile Service
revere_mobile_shortcode_number | string   | Shortcode Number that the subscriber interacts with.
status                         | string   | Status of Service, only Active will be allowed to be used
createdAt                      | datetime | Automatically generated date/time when user is created.
updatedAt                      | datetime | Automatically updated date/time when user is updated.

## The Revere Mobile Flow Object
Attribute                      | Type     | Description
-----------------------------  | -------- | -----------
id                             | ObjectId | Unique ID for the Mobile Flow.
name                           | string   | Name for the Mobile Service
revere_mobile_shortcode_number | string   | Shortcode Number that the subscriber interacts with.
revere_mobile_service_id       | ObjectId | Unique ID for the Mobile Service.
created_at                     | datetime | Automatically generated date/time when user is created.
updated_at                     | datetime | Automatically updated date/time when user is updated.

## The Terms and Conditions Object
Attribute                       | Type     | Description
------------------------------  | -------- | -----------
client_shortname                | string | Short Legal name of the user or user of Revere Mobile.
shortcode_number                | string | Shortcode Number that the subscriber interacts with.
public_terms_and_conditions_url | string | Endpoint for the Terms & Conditions Link
html                            | string | HTML String to be used with a Revere Mobile Signup Form


## Get All Revere Mobile Services

### HTTP Request
`GET https://sync.revmsg.net/api/revere_mobile/services`

```shell
curl -X GET \
  https://sync.revmsg.net/api/revere_mobile/services \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'authorization: Bearer <token>' \
  -H 'content-type: application/json'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sync.revmsg.net/api/revere_mobile/services',
  headers: 
   { 'content-type': 'application/json',
     accept: 'application/vnd.sync.v2+json',
     authorization: 'Bearer <token>' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});


```

> Will reply with a list of services

```json
[
    {
        "updatedAt": "2017-10-27T08:37:25.680Z",
        "createdAt": "2016-10-07T21:26:39.834Z",
        "name": "Example Mobile Service",
        "revere_mobile_shortcode_number": "225568",
        "status": "Active",
        "id": "57f8130f997eaf000a5baae2"
    },
    {
        "updatedAt": "2017-11-01T12:33:15.801Z",
        "createdAt": "2017-11-01T12:33:15.801Z",
        "name": "Example 2 Mobile Service",
        "revere_mobile_shortcode_number": "62262",
        "status": "Active",
        "id": "19f9rf0b2b35d2000d9b21cd"
    }
]
```

## Get One Mobile Service By Id

### HTTP Request
`GET https://sync.revmsg.net/api/revere_mobile/services/{id}`

### Query Parameters

Parameter      | Type      | Description
-------------- | -------   | -----------
id             | ObjectId  | The id of the service.

```shell
curl -X GET \
  https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'authorization: Bearer <token>' \
  -H 'content-type: application/json'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd',
  headers: 
   { 'content-type': 'application/json',
     accept: 'application/vnd.sync.v2+json',
     authorization: 'Bearer <token>' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});


```

> Will reply with one service

```json
{
  "updatedAt": "2017-11-01T12:33:15.801Z",
  "createdAt": "2017-11-01T12:33:15.801Z",
  "name": "Example 2 Mobile Service",
  "revere_mobile_shortcode_number": "62262",
  "status": "Active",
  "id": "19f9rf0b2b35d2000d9b21cd"
}
```

## Get A Service's Mobile Flows 

### HTTP Request
`GET https://sync.revmsg.net/api/revere_mobile/services/{id}/mobile_flows`


```shell
curl -X GET \
  https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd/mobile_flows \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'authorization: Bearer <token>' \
  -H 'content-type: application/json'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd/mobile_flows',
  headers: 
   { 'content-type': 'application/json',
     accept: 'application/vnd.sync.v2+json',
     authorization: 'Bearer <token>' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> Will reply with mobile flows

```json
[
    {
        "name": "Example Flow 1",
        "created_at": "2017-10-31T16:01:59.576Z",
        "updated_at": "2017-10-31T16:01:59.576Z",
        "id": "16f89542e4b0e9c3e9d6ca7a"
    },
    {
        "name": "Example Flow 2",
        "created_at": "2017-10-31T16:01:16.589Z",
        "updated_at": "2017-10-31T16:01:16.589Z",
        "id": "16f8916ae4b0e9c3e9d67b2e"
    },
    {
        "name": "Example Flow 3",
        "created_at": "2017-10-31T16:01:16.605Z",
        "updated_at": "2017-10-31T16:01:16.605Z",
        "id": "16f89428e4b0e9c3e9d6c72c"
    },
    {
        "name": "Example Flow 4",
        "created_at": "2017-10-31T16:01:16.640Z",
        "updated_at": "2017-10-31T16:01:16.640Z",
        "id": "16f67580e4b0fd80e639e64b"
    },
    {
        "name": "Example Flow 5",
        "created_at": "2017-10-31T16:01:16.671Z",
        "updated_at": "2017-10-31T16:01:16.671Z",
        "id": "16f67f62e4b0fd80e63a0725"
    }
]

```

### Get Revere Mobile Flow Info

It is also possible to trace back a mobile flow to it's service. This is useful for getting the Terms & Conditions for a
Revere Mobile Service.

### HTTP Request
`GET https://sync.revmsg.net/api/revere_mobile/mobile_flows/{id}`

### Query Parameters

Parameter      | Type      | Description
-------------- | -------   | -----------
id             | ObjectId  | The id of the Mobile Flow.

```shell
curl -X GET \
  https://sync.revmsg.net/api/revere_mobile/mobile_flows/16f89542e4b0e9c3e9d6ca7a \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'authorization: Bearer <token>' \
  -H 'content-type: application/json'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sync.revmsg.net/api/revere_mobile/mobile_flows/16f89542e4b0e9c3e9d6ca7a',
  headers: 
   { 'content-type': 'application/json',
     authorization: 'Bearer <token>',
     accept: 'application/vnd.sync.v2+json' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> Will reply with 

```json
{
    "name": "Example Flow 1",
    "id": "16f89542e4b0e9c3e9d6ca7a",
    "revere_mobile_service_id": "19f9rf0b2b35d2000d9b21cd",
    "revere_mobile_shortcode_number": "62262"
}
```

## Get A Service's Terms & Conditions
This is the entry point to retrive a Revere Mobile Services's Terms & Conditions. 
This requires a Revere Mobile Service to operate.

### HTTP Request
`GET https://sync.revmsg.net/api/revere_mobile/services/{id}/terms_and_conditions`

```shell
curl -X GET \
  https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd/terms_and_conditions \
  -H 'accept: application/vnd.sync.v2+json' \
  -H 'authorization: Bearer <token>' \
  -H 'content-type: application/json'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sync.revmsg.net/api/revere_mobile/services/19f9rf0b2b35d2000d9b21cd/terms_and_conditions',
  headers: 
   { 'content-type': 'application/json',
     accept: 'application/vnd.sync.v2+json',
     authorization: 'Bearer <token>' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```
> Will reply with the Terms And Conditions

```json
{
    "client_shortname": "Example Client",
    "shortcode_number": "62262",
    "public_terms_and_conditions_url": "https://sync.revmsg.net/public/terms-and-conditions/8b242a3e-3e33-4954-8b01-64a92c9f671c/62262",
    "html": "<p>Mobile alerts from Example Client messages. Msg &amp; data rates may apply.<b>Text STOP to 62262 to stop receiving messages.Text HELP to 62262 for more information.</b><br> <a href=\"https://sync.revmsg.net/public/terms-and-conditions/8b242a3e-3e33-4954-8b01-64a92c9f671c/62262\" target=\"_blank\">Terms &amp; Conditions</a>"
}
```