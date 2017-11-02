# Constitutent

**Note: This endpoint does not require Authentication and is designed for public use.**

**Note: This endpoint is not OSDI enabled.**

Constituents are a legacy actor in Sync and actions by triggers are preformed on them.
It is possible to create constituents with `GET` and `PUT` requests but this method is highly discouraged and only exists for backwards compatibility with V1. All constituents should be created using the `POST` method. This endpoint is used by Sync V2 forms and should be used if creating a custom interaction with Sync V2.

### HTTP Request
`POST https://sync.revmsg.net/constituent/{access_token}`

## Create a constituent
```shell
curl -X POST \
  https://sync.revmsg.net/constituent/ba6dc8c06b3aa6a461fbae850a26dda5 \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
	"name":"Steve Bob",
	"firstname":"Steve",
	"lastname":"Bob",
	"address":"555 Fake St.",
	"address_two":"APT 24",
	"city":"Seattle",
	"state":"WA",
	"zipcode":"98045",
	"email":"steve@steve.com",
	"home_phone":"1-555-555-5555",
	"msisdn":"1-555-555-5555",
	"employer":"Steve Company Inc",
	"metadata": {
		"source":"facebook",
		"emailOptInStatus":"I"
		},
	"tags":"amazingpeople2016"
}'
```

```javascript
var request = require("request");

var options = { method: 'POST',
  url: 'https://sync.revmsg.net/constituent/ba6dc8c06b3aa6a461fbae850a26dda5',
  headers: 
   { 'postman-token': 'e072e825-97a3-6953-5641-a75badc9dfb6',
     'content-type': 'application/json',
     'cache-control': 'no-cache' },
  body: 
   { name: 'Steve Bob',
     firstname: 'Steve',
     lastname: 'Bob',
     address: '555 Fake St.',
     address_two: 'APT 24',
     city: 'Seattle',
     state: 'WA',
     zipcode: '98045',
     email: 'steve@steve.com',
     home_phone: '1-555-555-5555',
     msisdn: '1-555-555-5555',
     employer: 'Steve Company Inc',
     metadata: { source: 'facebook', emailOptInStatus: 'I' },
     tags: 'amazingpeople2016' },
  json: true };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

> JSON response of on create

```json
{
  "error":false,
  "message":"Contact accepted.",
  "id":"57d723cbd9dc8cdc5ad00191"
}
```

### Provide an access token to send with constituent data

| Parameter      | Type   | Required | Description             
| -------------- | ------ | -------- | ------------------------------- 
| access_token   | String | True     | Access Token Hash  

At least one paramater is required to post data. Below are the allowed fields for a constituent. **The tag parameter is required to activate the triggers which will forward information to Sync's integrations.** Each tag can be a string or an array of strings.

### Post Parameters

| Properties          | Type     | Required | Description |
| --------------------| -------- | -------- | ---------------------------------------------------------------------------------------- |
| name                | String   | False    | Full name, will be created from `firstname` and `lastname` automatically if possible.    |
| firstname           | String   | False    | First Name of Constituent |
| lastname            | String   | False    | Last Name of Constituent |
| address             | String   | False    | Primary Street Address |
| address_two         | String   | False    | Secondary Street Address|
| city                | String   | False    | City of Constituent |
| state               | String   | False    | Two Char String ( IE: WA ) |
| zipcode             | String   | False    | Five Digit Zip Code and four seperated by `-`. `98036` or `98036-1513` are OK. |
| email               | String   | False    | Email of Constituent  |
| work_email          | String   | False    | Work Email of Constituent  |
| phone               | String   | False    | Phone of Constituent, will populate msisdn when phone provided. |
| msisdn              | String   | False    | Mobile Phone number of Constituent, gets populated by `phone` if only phone is provided. |
| work_phone          | String   | False    | Work Phone number of Constituent |
| home_phone          | String   | False    | Home Phone number of Constituent |
| employer            | String   | False    | Employer of Constituent |
| work_address 	      | String   | False    | Work address of Constituent. |
| work_address_two    | String   | False    | Work address, second line of Constituent |
| work_city           | String   | False    | Work city of Constituent. | 
| work_state          | String   | False    | Work State, TWO Char String (IE: WA). |
| work_zipcode 	      | String   | False    | Work Zip Code, a five digit zip code and four seperated by `-`. `98036` or `98036-1513` are OK. |
| mail_address        | String   | False    | Mail address of Constituent. |
| mail_address_two    | String   | False    | Mail address, second line of Constituent |
| mail_city           | String   | False    | Mail city of Constituent. | 
| mail_state          | String   | False    | Mail State, TWO Char String (IE: WA). |
| mail_zipcode        | String   | False    | Mail Zip Code, a five digit zip code and four seperated by `-`. `98036` or `98036-1513` are OK. |
| vote_address        | String   | False    | Voter address of Constituent. |
| vote_address_two    | String   | False    | Voter address, second line of Constituent |
| vote_city           | String   | False    | Voter city of Constituent. | 
| vote_state          | String   | False    | Voter State, TWO Char String (IE: WA). |
| vote_zipcode        | String   | False    | Voter Zip Code, a five digit zip code and four seperated by `-`. `98036` or `98036-1513` are OK. |
| metadata            | Object   | False    | Metadata object (see table), IE: `source`:`string` for an ActionKit integration |
| tags                | String   | False    | Can be one String or an Array of Strings used to trigger actions setup inside of Sync.  |



### Metadata Object

| Properties | Type     | Required | Description |
| ----------------------| -------- | ---------| ------------------------------------------------------------------------- |
| source                | string   | False    | A string, such as `facebook`, `twitter`, `EveryActionForm` etc.           |
| preferredPhone        | string   | False    | Must be `msisdn`, `work_phone`, or `home_phone` and field must be present.|
| preferredEmail        | string   | False    | Must be `email` or `work_email` and field must be present.                |
| phoneOptInStatus      | string   | False    | Must be `I` for in or `O` for out. Default is `O`.                        |
| emailOptInStatus      | string   | False    | Must be `I` for in or `O` for out. Default is `O`                         |
