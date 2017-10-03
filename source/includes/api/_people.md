# People

People are the main resource in the Revere Sync. This is the main entry point for Sync and where information is passed and retrivied.

## Person Signup Helper

This route is desiged to create or update a person. The match is based on four paramaters, `given_name`, `family_name`, an `email_address` and a `phone_number`. If a person is found based on any of this information sync will return with updated person, otherwise the person will be created. The  `postal_addresses` field and `profiles` fields will create additions. This means when new information is provided it is saved so be careful when creating `postal_address` fields and `profiles`. The `email_addresses` and `phone_numbers` fields will match on `address` for `email_address` and `number` for `phone_numbers`. Those will then update the details in respect to resource.

### Triggers

Currently we support an auto respoonse using a `mobile_flow_id`. When provided this trigger will subscribe the `primary_phone_number` to a mobile list.

`POST https://sync.revmsg.net/api/people/person_signup_helper`

```shell
curl -X POST \
  https://sync.revmsg.net/api/people/person_signup_helper \
  -H 'Accept: application/vnd.sync.v2+hal+json' \
  -H 'Authorization: Bearer <token>' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
  "person":{
    "given_name":"John",
    "family_name":"Doe",
    "identifiers": [
        "vanId:252"
    ],
    "party_identification":"Democratic",
    "custom_fields":{
      "some_string":"here",
      "boolean_value":false,
      "number_value":15
    },
    "birthdate":{
        "year": 1992,
        "month": 11,
        "day": 25
    },
    "postal_addresses":[
      {
        "primary":true,
        "locality":"Seattle",
        "region":"WA",
        "addressLine1":"515 Example St.",
        "postal_code":"98036",
        "address_type":"Home"
        
      }
    ],
    "phone_numbers":[
        {
          "number":"+1234567890",
          "number_type":"Mobile",
          "primary":true
        }
      ],
    "email_addresses":[
        {
          "address":"john@doe.com",
          "address_type":"Work",
          "primary":true
        }
      ],
    "profiles":[
      {
        "url":"https://twitter.com/johndoe15",
        "handle":"johndoe15",
        "profile_provider":"twitter"
      }
    ],
    "triggers":{
      "autoresponse":{
        "enabled":true,
        "revere_mobile_flow_trigger":{
          "params":{
            "mobile_flow_id":"58c1vcfae4b0569e60c923fd"
          }
        }
      }
    }  
  }
}'
```

```javascript
var request = require("request");

var options = { method: "POST",
  url: "https://sync.revmsg.net/api/people/person_signup_helper",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" },
  body: 
   {
    person: {
      given_name:"John",
      family_name:"Doe",
      identifiers: [
          "vanI:252"
      ],
      party_identification:"Democratic",
      custom_fields:{
          some_string:"here",
          boolean_value:false,
          number_value:15
      },
      birthdate:{
        year: 1992,
        month: 11,
        day: 25
      },
      postal_addresses:[
          {
              primary:true,
              locality:"Seattle",
              region:"WA",
              addressLine1:"515 Example St.",
              postal_code:"98036",
              address_type:"Home"
              
          }
      ],
      phone_numbers:[
              {
                  number:"+1234567890",
                  number_type:"Mobile",
                  primary:true
              }
          ],
      email_addresses:[
              {
                  address:"john@doe.com",
                  address_type:"Work",
                  primary:true
              }
          ],
          
      profiles:[
          {
              url:"http://twitter.com/johndoe15",
              handle:"johndoe15",
              profile_provider:"twitter"
          }
      ],
      triggers: {
        autoresponse: {
          enabled: true,
          revere_mobile_flow_trigger: {
            params: {
              mobile_flow_id:"58c1vcfae4b0569e60c923fd"
            }
          }
        }
      }
    } 
   },
  json: true
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});


```

> The above returns JSON response of on create or update:

```json
{
  "_links": {
    "self": [
      {
        "href": "/v2/api/people"
      },
      {
        "href": "http://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323"
      }
    ]
  },
  "revere_sync_id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "identifiers": [
    "vanId:252",
    "revere_sync:ae87ccde-7d82-4554-bded-56f305a4d323"
  ],
  "id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "family_name": "Doe",
  "given_name": "John",
  "additional_name": null,
  "honorific_prefix": null,
  "origin_system": "revere_sync",
  "party_identification": "Democratic",
  "preferred_language": "en",
  "source": null,
  "birthdate": {
    "year": 1999,
    "month": 11,
    "day": 22
  },
  "employer": null,
  "gender": null,
  "custom_fields": {
    "some_string": "here",
    "boolean_value": false,
    "number_value": 15
  },
  "ngp_van_sync_status": null,
  "mobile_sync_status": null,
  "created_at": "2017-05-23T09:30:49.569Z",
  "updated_at": "2017-05-23T09:30:49.569Z",
  "email_addresses": [
    {
      "address_type": "Work",
      "status": null,
      "primary": true,
      "address": "john@doe.com",
      "email_address_type": "work",
      "email_subscription_status": null,
      "updated_at": "2017-05-23T09:30:49.602Z"
    }
  ],
  "phone_numbers": [
    {
      "number_type": "Mobile",
      "primary": true,
      "number": "+1234567890",
      "description": null,
      "operator": null,
      "country": null,
      "sms_capable": false,
      "do_not_call": false,
      "phone_number_type": "mobile",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ],
  "postal_addresses": [
    {
      "location": {
        "latitude": null,
        "longitude": null,
        "accuracy": null
      },
      "address_type": "Home",
      "status": "Potential",
      "primary": true,
      "venue": null,
      "addressLine1": "515 Example St.",
      "addressLine2": null,
      "addressLine3": null,
      "locality": "Seattle",
      "region": "WA",
      "postal_code": 98036,
      "postal_code_plus_4": null,
      "country": "US",
      "language": "en",
      "latitude": null,
      "longitude": null,
      "accuracy": null,
      "last_verified_date": null,
      "postal_address_type": "home",
      "postal_address_status": "potential",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ]
}
```

### Post Parameters

Properties            | Type    | Required  | Description
--------------------- | ------- |---------- |-----------
given_name            | string  |   true    | First Name or Given Name of a Person.
family_name           | string  |   true    | Family or Last Name of a Person.
identifiers           | array   |   false   | External ID, can provide a list  
party_identification  | string  |   false   | Democratic, Republican, Independent, Other.
custom_fields         | object  |   false   | Object of custom fields IE: `{ foo:bar }`
birthdate             | object  |   false   | Object of OSDI birthday IE: `{ year: 2000, month:1, day:1 }`
email_addresses       | array   |   true    | Array of at least one primary Email object.
phone_numbers         | array   |   true    | Array of at least one Phone Number object. 
postal_addresses      | array   |   false   | Array of at least one Phone Number object.
profiles              | array   |   false   | Array of profile objects.
triggers              | object  |   false   | Object with autoresponse triggers with params.

Note: `primary:true` should be the first item in the list of `email_addresses`, `phone_numbers`, `postal_addresses`.

### Email Address

Properties                | Type    | Required  | Description
------------------------- | ------- |---------- |---------------------------------------
address_type              | string  |   false   | Can be "Personal", "Work", "Other".
status                    | string  |   false   | Can be "Subscribed", "Unsubscribed".
primary                   | boolean |   false   | Can be true or false if primary email address.
address                   | string  |   true    | A valid email address.

### Phone Number

Properties        | Type    | Required  | Description
----------------- | ------- |---------- |---------------------------------------
number_type       | string  |   false   | Can be "Home", "Work", "Mobile", "Other", "Daytime", "Evening", "Fax".
primary           | boolean |   false   | Can be true or false if primary phone number.
number            | string  |   true    | E.164 formatted US phone number.
description       | string  |   false   | Number description, max length is 50 chars.
operator          | string  |   false   | Network Carrier.
sms_capable       | boolean |   false   | True if the number is able to receive sms and mms messages.
do_not_call       | boolean |   false   | If number should not be called.
country           | string  |   false   | The country code according to ISO 3166-1 Alpha-2.


### Postal Addresses

Properties         | Type    | Required  | Description
-----------------  | ------- |---------- |---------------------------------------
primary            | boolean | false     | True if this is as a primary address, can only have one primary address
address_type       | string  | false     | The type of address. One of “Home”, “Work”, or “Mailing”.
venue              | string  | false     | Optional venue name at the address, useful for names of buildings. ex: Smith Hall)
addressLine1       | string  | false     | Primary Address Line 
addressLine2       | string  | false     | Secondary Address Line
addressLine3       | string  | false     | Final Address Line
locality           | string  | false     | A city or other local administrative area.
region             | string  | false     | State or subdivision codes according to ISO 3166-2 Final 2 alpha digits). 
postal_code        | string  | false      | Five or Nine digit US postal code.
country            | string  | false     | The country code according to ISO 3166-1 Alpha-2.
language           | string  | false     | Language in which the address is recorded – language code according to ISO 639. 
location           | object  | false     | `{ latitude: number,  longitude: number, accuracy:"Rooftop" or "Approximate" }`
status             | string  | false     | The type of address. One of “Home”, “Work”, or “Mailing”.
last_verified_date | date    | false     | Date last verified of the address. 

### Profiles

Properties           | Type    | Required  | Description
-------------------- | ------- |---------- |---------------------------------------
url                  | string  | false     | Social Profile URL
provider             | string  | false     | Social Profile Provider "Facebook", "Twitter", "Other"
id                   | string  | false     | External Profile id
handle               | string  | false     | Social Profile Media Handle

## Find Or Create a Person

This route is desiged to create or match a person. The match is based on four paramaters, `given_name`, `family_name`, an `email_address` and a 
`phone_number`. If a person is found based on any of this information sync will return with the full id of the person, otherwise the person will be created.

A person will be returned with standard OSDI fields but will also contain extra due to the naming scheme of our internal systems. Both can be used but OSDI 1.1 fields are recomended.


`POST https://sync.revmsg.net/api/people`

```shell
curl -X POST \
  https://sync.revmsg.net/api/people \
  -H 'Accept: application/vnd.sync.v2+hal+json' \
  -H 'Authorization: Bearer <token>' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
	"given_name":"John",
	"family_name":"Doe",
	"identifiers": [
    	"vanId:252"
	],
	"party_identification":"Democratic",
	"custom_fields":{
		"some_string":"here",
		"boolean_value":false,
		"number_value":15
	},
	"birthdate":{
      "year": 1992,
      "month": 11,
      "day": 25
	},
	"postal_addresses":[
		{
			"primary":true,
			"locality":"Seattle",
			"region":"WA",
			"addressLine1":"515 Example St.",
			"postal_code":"98036",
			"address_type":"Home"
			
		}
	],
	"phone_numbers":[
			{
				"number":"+1234567890",
				"number_type":"Mobile",
				"primary":true
			}
		],
	"email_addresses":[
			{
				"address":"john@doe.com",
				"address_type":"Work",
				"primary":true
			}
		],
		
	"profiles":[
		{
			"url":"https://twitter.com/johndoe15",
			"handle":"johndoe15",
			"profile_provider":"twitter"
		}
	]
}'
```


```javascript
var request = require("request");

var options = { method: "POST",
  url: "https://sync.revmsg.net/api/people",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" },
  body: 
   {
    given_name:"John",
    family_name:"Doe",
    identifiers: [
        "vanI:252"
    ],
    party_identification:"Democratic",
    custom_fields:{
        some_string:"here",
        boolean_value:false,
        number_value:15
    },
    birthdate:{
      year: 1992,
      month: 11,
      day: 25
    },
    postal_addresses:[
        {
            primary:true,
            locality:"Seattle",
            region:"WA",
            addressLine1:"515 Example St.",
            postal_code:"98036",
            address_type:"Home"
            
        }
    ],
    phone_numbers:[
            {
                number:"+1234567890",
                number_type:"Mobile",
                primary:true
            }
        ],
    email_addresses:[
            {
                address:"john@doe.com",
                address_type:"Work",
                primary:true
            }
        ],
        
    profiles:[
        {
            url:"http://twitter.com/johndoe15",
            handle:"johndoe15",
            profile_provider:"twitter"
        }
    ]
   },
  json: true
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> The above returns JSON response of on create:

```json
{
  "_links": {
    "self": [
      {
        "href": "/v2/api/people"
      },
      {
        "href": "http://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323"
      }
    ]
  },
  "revere_sync_id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "identifiers": [
    "vanId:252",
    "revere_sync:ae87ccde-7d82-4554-bded-56f305a4d323"
  ],
  "id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "family_name": "Doe",
  "given_name": "John",
  "additional_name": null,
  "honorific_prefix": null,
  "origin_system": "revere_sync",
  "party_identification": "Democratic",
  "preferred_language": "en",
  "source": null,
  "birthdate": {
    "year": 1999,
    "month": 11,
    "day": 22
  },
  "employer": null,
  "gender": null,
  "custom_fields": {
    "some_string": "here",
    "boolean_value": false,
    "number_value": 15
  },
  "ngp_van_sync_status": null,
  "mobile_sync_status": null,
  "created_at": "2017-05-23T09:30:49.569Z",
  "updated_at": "2017-05-23T09:30:49.569Z",
  "email_addresses": [
    {
      "address_type": "Work",
      "status": null,
      "primary": true,
      "address": "john@doe.com",
      "email_address_type": "work",
      "email_subscription_status": null,
      "updated_at": "2017-05-23T09:30:49.602Z"
    }
  ],
  "phone_numbers": [
    {
      "number_type": "Mobile",
      "primary": true,
      "number": "+1234567890",
      "description": null,
      "operator": null,
      "country": null,
      "sms_capable": false,
      "do_not_call": false,
      "phone_number_type": "mobile",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ],
  "postal_addresses": [
    {
      "location": {
        "latitude": null,
        "longitude": null,
        "accuracy": null
      },
      "address_type": "Home",
      "status": "Potential",
      "primary": true,
      "venue": null,
      "addressLine1": "515 Example St.",
      "addressLine2": null,
      "addressLine3": null,
      "locality": "Seattle",
      "region": "WA",
      "postal_code": 98036,
      "postal_code_plus_4": null,
      "country": "US",
      "language": "en",
      "latitude": null,
      "longitude": null,
      "accuracy": null,
      "last_verified_date": null,
      "postal_address_type": "home",
      "postal_address_status": "potential",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ]
}
```

> The above returns JSON response of on match:

```json
{
  "_links": {
    "self": [
      {
        "href": "/v2/api/people"
      },
      {
        "href": "http://sync.revmsg.net/api/people/df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd"
      }
    ]
  },
  "revere_sync_id": "df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd",
  "message": "Person Matched, use a PUT to update with new information."
}
```

<aside class="notice">
Revere Sync requires at least the four main parameters to create a person.
</aside>


### Post Parameters

Post Parameters    | Type    | Required  | Description
------------------ | ------- |---------- |-----------
given_name         | string  |   true    | First Name or Given Name of a Person.
family_name        | string  |   true    | Family or Last Name of a Person.
email_addresses    | array   |   true    | Array of at least one primary Email object.
phone_numbers      | array   |   true    | Array of at least one Phone Number object. 
postal_addresses   | array   |   false   | Array of at least one Phone Number object.

Note: `primary:true` should be the first item in the list of `email_addresses`, `phone_numbers`, `postal_addresses`.

## Get Page of People 

This route will allow you to fetch up to 10 person records at a time. You can increment the pages 
by providing a `?page=<number>` query string.

`GET https://sync.revmsg.net/people/:revere_sync_id`

```shell
curl "https://sync.revmsg.net/api/people"
  -H "Content-Type: application/json",
  -H "Accept: application/vnd.sync.v2+json",
  -H "Authorization: <token>"
```

```javascript
var request = require("request");

var options = { method: "GET",
  url: "https://sync.revmsg.net/api/people",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" 
   }
};
```

> or by page

```shell
curl "https://sync.revmsg.net/api/people?page=2"
  -H "Content-Type: application/json",
  -H "Accept: application/vnd.sync.v2+json",
  -H "Authorization: <token>"
```


```javascript
var request = require("request");

var options = { method: "GET",
  url: "https://sync.revmsg.net/api/people?page=2",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" 
   }
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> Will reply with a list of people

```json
{
  "_links": {
    "self": {
      "href": [
        "https://sync.revmsg.net/v2/api/people/df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd"
      ]
    },
    "next": {
      "href": "https://sync.revmsg.net/v2/api/people?page="
    },
    "curies": [
      {
        "name": "revere_sync",
        "href": "/rels/Revolution Messaging/{rel}",
        "templated": true
      }
    ]
  },
  "total_pages": 1,
  "per_page": 10,
  "page": 1,
  "next": null,
  "total_records": 1,
  "_embedded": {
    "revere_sync:people": {
      "_links": {
        "self": {
          "href": "https://sync.revmsg.net/v2/api/people/df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd"
        }
      },
      "revere_sync_id": "df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd",
      "identifiers": [
        "vanId:252",
        "revere_sync:df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd"
      ],
      "birthdate": {
        "year": 1999,
        "month": 11,
        "day": 22
      },
      "gender": "",
      "custom_fields": {
        "some_string": "here",
        "boolean_value": false,
        "number_value": 15
      },
      "ngp_van_sync_status": null,
      "mobile_sync_status": null,
      "id": "df7ef2d4-12b9-45eb-ba8a-aa958a4c8ffd",
      "family_name": "Person",
      "given_name": "Test",
      "additional_name": null,
      "honorific_prefix": null,
      "origin_system": "revere_sync",
      "party_identification": "Democratic",
      "preferred_language": "en",
      "source": null,
      "employer": null,
      "occupation": null,
      "gender_identity": null,
      "createdAt": "2017-06-30T02:13:05.377Z",
      "updatedAt": "2017-06-30T02:13:05.377Z",
      "created_at": "2017-06-30T02:13:05.377Z",
      "updated_at": "2017-06-30T02:13:05.377Z",
      "postal_addresses": [
        {
          "location": {
            "latitude": null,
            "longitude": null,
            "accuracy": null
          },
          "address_type": "Home",
          "status": "Potential",
          "primary": true,
          "venue": null,
          "addressLine1": "515 Example St.",
          "addressLine2": null,
          "addressLine3": null,
          "locality": "Seattle",
          "region": "WA",
          "postal_code": 98036,
          "postal_code_plus_4": null,
          "country": "US",
          "language": "en",
          "latitude": null,
          "longitude": null,
          "accuracy": null,
          "last_verified_date": null,
          "postal_address_type": "home",
          "postal_address_status": "potential",
          "updated_at": "2017-05-23T09:30:49.604Z"
        }
      ],
      "email_addresses": [
        {
          "address_type": "Work",
          "status": null,
          "primary": true,
          "address": "john@doe.com",
          "email_address_type": "work",
          "email_subscription_status": null,
          "updated_at": "2017-05-23T09:30:49.602Z"
        }
      ],
      "phone_numbers": [
        {
          "number_type": "Mobile",
          "primary": true,
          "number": "+1234567890",
          "description": null,
          "operator": null,
          "country": null,
          "sms_capable": false,
          "do_not_call": false,
          "phone_number_type": "mobile",
          "updated_at": "2017-05-23T09:30:49.604Z"
        }
      ],
      "profiles": [
        {
          "profile_provider": "Twitter",
          "id": "bc603110-1583-4620-9201-f619300b394b",
          "external_profile_id": null,
          "url": "https://twitter.com/johndoe15",
          "handle": "johndoe15",
          "updated_at": "2017-06-30T02:13:05.421Z"
        }
      ]
    }
  }
}
```


Parameter      | Type    | Description
-------------- | ------- | -----------
page           | number  | The page to fetch next

## Get One Person By Id

`GET https://sync.revmsg.net/people/:revere_sync_id`

### Query Parameters

Parameter      | Type    | Description
-------------- | ------- | -----------
revere_sync_id | string  | The id of the person inside of Revere Sync.

```shell
curl "https://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323"
  -H "Content-Type: application/json",
  -H "Accept: application/vnd.sync.v2+json",
  -H "Authorization: <token>"
```

```javascript
var request = require("request");

var options = { method: "POST",
  url: "https://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" }
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> The above returns JSON response of:

```json
{
  "_links": {
    "self": {
      "href": "/v2/api/people/ae87ccde-7d82-4554-bded-56f305a4d323"
    }
  },
  "revere_sync_id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "identifiers": [
    "vanId:252",
    "revere_sync:ae87ccde-7d82-4554-bded-56f305a4d323"
  ],
  "id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "family_name": "Doe",
  "given_name": "John",
  "additional_name": null,
  "honorific_prefix": null,
  "origin_system": "revere_sync",
  "party_identification": "Democratic",
  "preferred_language": "en",
  "source": null,
  "birthdate": {
    "year": 1999,
    "month": 11,
    "day": 22
  },
  "employer": null,
  "gender": null,
  "custom_fields": {
    "some_string": "here",
    "boolean_value": false,
    "number_value": 15
  },
  "ngp_van_sync_status": null,
  "mobile_sync_status": null,
  "created_at": "2017-05-23T09:30:49.569Z",
  "updated_at": "2017-05-23T09:30:49.569Z",
  "email_addresses": [
    {
      "address_type": "Work",
      "status": null,
      "primary": true,
      "address": "john@doe.com",
      "email_address_type": "work",
      "email_subscription_status": null,
      "updated_at": "2017-05-23T09:30:49.602Z"
    }
  ],
  "phone_numbers": [
    {
      "number_type": "Mobile",
      "primary": true,
      "number": "+1234567890",
      "description": null,
      "operator": null,
      "country": null,
      "sms_capable": false,
      "do_not_call": false,
      "phone_number_type": "mobile",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ],
  "postal_addresses": [
    {
      "location": {
        "latitude": null,
        "longitude": null,
        "accuracy": null
      },
      "address_type": "Home",
      "status": "Potential",
      "primary": true,
      "venue": null,
      "addressLine1": "515 Example St.",
      "addressLine2": null,
      "addressLine3": null,
      "locality": "Seattle",
      "region": "WA",
      "postal_code": 98036,
      "postal_code_plus_4": null,
      "country": "US",
      "language": "en",
      "latitude": null,
      "longitude": null,
      "accuracy": null,
      "last_verified_date": null,
      "postal_address_type": "home",
      "postal_address_status": "potential",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ]
}
```

## Update One Person

`PUT https://sync.revmsg.net/people/:revere_sync_id`

<aside class="notice">
Revere requires at least four main parameters to create a constituent.
</aside>

```shell
curl -X PUT \
  https://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323 \
  -H 'Accept: application/vnd.sync.v2+hal+json' \
  -H 'Authorization: Bearer <token>' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
  "given_name":"John",
  "family_name":"Doe",
  "identifiers": [
      "vanId:252",
      "salsaId:54654-56456-46262"
  ],
  "party_identification":"Democratic",
  "custom_fields":{
    "some_string":"here",
    "boolean_value":true,
    "number_value":15,
    "new_field":"wow"
  },
  "postal_addresses":[
    {
      "locality": "Seattle",
      "region": "WA",
      "addressLine1": "Po Box",
      "addressLine2": "15",
      "postal_code": "98036",
      "address_type":"Mailing"
    }   
  ],
  "phone_numbers":[
      {
        "number":"+19876543321",
        "number_type":"Home",
        "sms_capable":false
      }
  ],
  "email_addresses":[
      {
        "address":"joe_awesome@gmail.com",
        "address_type":"Personal"
      }
  ]
}'
```

```javascript
var request = require("request");

var options = { method: "POST",
  url: "https://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323",
  headers: 
   { "cache-control": "no-cache",
     "content-type": "application/json",
     "accept": "application/vnd.sync.v2+hal+json",
     "authorization": "Bearer <token>" },
  body: {
    given_name:"John",
    family_name:"Doe",
    identifiers: [
        "vanId:252",
        "salsaId:54654-56456-46262"
    ],
    party_identification:"Democratic",
    custom_fields:{
      some_string:"here",
      boolean_value:true,
      number_value:15,
      new_field:"wow"
    },
    postal_addresses:[
      {
        locality: "Seattle",
        region: "WA",
        addressLine1: "Po Box",
        addressLine2: "15",
        postal_code: "98036",
        address_type:"Mailing"
      }   
    ],
    phone_numbers:[
        {
          number:"+19876543321",
          number_type:"Home",
          sms_capable:false
        }
    ],
    email_addresses:[
        {
          address:"joe_awesome@gmail.com",
          address_type:"Personal"
        }
    ] 
  }
};
```

> The above returns JSON response of:

```json
{
  "_links": {
    "self": [
      {
        "href": "/v2/api/people"
      },
      {
        "href": "http://sync.revmsg.net/api/people/ae87ccde-7d82-4554-bded-56f305a4d323"
      }
    ]
  },
  "revere_sync_id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "identifiers": [
    "vanId:252",
    "salsaId:54654-56456-46262",
    "revere_sync:ae87ccde-7d82-4554-bded-56f305a4d323"
  ],
  "id": "ae87ccde-7d82-4554-bded-56f305a4d323",
  "family_name": "Doe",
  "given_name": "John",
  "additional_name": null,
  "honorific_prefix": null,
  "origin_system": "revere_sync",
  "party_identification": "Democratic",
  "preferred_language": "en",
  "source": null,
  "birthdate": {
    "year": 1999,
    "month": 11,
    "day": 22
  },
  "employer": null,
  "gender": null,
  "custom_fields": {
    "some_string": "here",
    "boolean_value": false,
    "number_value": 15,
    "new_field":"wow"
  },
  "ngp_van_sync_status": null,
  "mobile_sync_status": null,
  "created_at": "2017-05-23T09:30:49.569Z",
  "updated_at": "2017-05-23T09:30:49.569Z",
  "email_addresses": [
    {
      "address_type": "Work",
      "status": null,
      "primary": true,
      "address": "john@doe.com",
      "email_address_type": "work",
      "email_subscription_status": null,
      "updated_at": "2017-05-23T09:30:49.602Z"
    },

    {
      "address_type": "Personal",
      "status": null,
      "primary": false,
      "address": "joe_awesome@gmail.com",
      "email_address_type": "personal",
      "email_subscription_status": null,
      "updated_at": "2017-05-23T09:30:49.603Z"
    },
  ],
  "phone_numbers": [
    {
      "number_type": "Mobile",
      "primary": true,
      "number": "+1234567890",
      "description": null,
      "operator": null,
      "country": null,
      "sms_capable": false,
      "do_not_call": false,
      "phone_number_type": "mobile",
      "updated_at": "2017-05-23T09:30:49.604Z"
    },
    {
      "number_type": "Home",
      "primary": false,
      "number": "+19876543321",
      "description": null,
      "operator": null,
      "country": null,
      "sms_capable": false,
      "do_not_call": false,
      "phone_number_type": "home",
      "updated_at": "2017-05-23T09:30:49.604Z"
    }
  ],
  "postal_addresses": [
    {
      "location": {
        "latitude": null,
        "longitude": null,
        "accuracy": null
      },
      "address_type": "Home",
      "status": "Potential",
      "primary": true,
      "venue": null,
      "addressLine1": "515 Example St.",
      "addressLine2": null,
      "addressLine3": null,
      "locality": "Seattle",
      "region": "WA",
      "postal_code": 98036,
      "postal_code_plus_4": null,
      "country": "US",
      "language": "en",
      "latitude": null,
      "longitude": null,
      "accuracy": null,
      "last_verified_date": null,
      "postal_address_type": "home",
      "postal_address_status": "potential",
      "updated_at": "2017-05-23T09:30:49.604Z"
    },
    {
      "location": {
        "latitude": null,
        "longitude": null,
        "accuracy": null
      },
      "address_type": "Home",
      "status": "Potential",
      "primary": false,
      "venue": null,
      "addressLine1": "Po Box",
      "addressLine2": "15",
      "addressLine3": null,
      "locality": "Seattle",
      "region": "WA",
      "postal_code": 98036,
      "postal_code_plus_4": null,
      "country": null,
      "language": "en",
      "latitude": null,
      "longitude": null,
      "accuracy": null,
      "last_verified_date": null,
      "postal_address_type": "home",
      "postal_address_status": "potential",
      "updated_at": "2017-05-23T09:30:49.605Z"
    }
  ]
}
```

### Post Parameters

Post Parameters  | Type    | Required  | Description
---------------  | ------- |---------- |-----------
given_name       | string  |   false   | First Name or Given Name of a Person.
family_name      | string  |   false   | Family or Last Name of a Person.
email_addresses  | array   |   false   | Array of at least one primary Email object. If only one is provided that becomes the primary.
phone_numbers    | array   |   false   | Array of at least one Phone Number object. If only one is provided that becomes the primary.
postal_addresses | array   |   false   | Array of at least one Phone Number object. If only one is provided that becomes the primary.
