# Persons

This is an api example. Here this is nested in a folder so we can reference parts of the doc that make sense. Keep these after Errors.

> To get people

```ruby
require 'people'

api = People::APIClient.authorize!('somekey')
```

```python
import people

api = people.authorize('somekey')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: somekey"
```

```javascript
const people = require('people');

let api = people.authorize('somekey');
```

> Make sure to replace `somekey` with your API key.

People uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: somekey`

<aside class="notice">
You must replace <code>somekey</code> with your personal API key.
</aside>