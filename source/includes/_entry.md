# Entry Point

This unauthenticated route is to be used to discover the OSDI Sync API. It will return the possible resources
to use with sync.


```shell
curl -X GET \
     "https://sync.revmsg.net/api" \
  -H 'accept: application/vnd.sync.v2+json' \
```


> The above returns JSON response of:

```json
{
  "_links": {
    "self": {
      "href": "/v2/api/"
    },
    "curies": [
      {
        "name": "revere_sync",
        "href": "/rels/Revolution Messaging/{rel}",
        "templated": true
      }
    ],
    "revere_sync:people": [
      {
        "href": "/v2/api/people"
      },
      {
        "href": "/v2/api/people/{id}",
        "templated": true
      },
      {
        "href": "/v2/api/people"
      }
    ]
  }
}
```