# Pagination

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const users = await briq.organization('your-organization').users({ per_page: 1 });
```

```shell
curl -i -u briq_api_token "https://www.givebriq.com/v0/organizations/your-organization/users?per_page=1"
```

> The response will include the appropriate `Link` HTTP headers if needed

```
Link: <http://briq.localhost:3000/v0/organizations/your-organization/users?page=2&per_page=1>; rel="next", <http://briq.localhost:3000/v0/organizations/your-organization/users?page=2&per_page=1>; rel="last"
```

Endpoints that return arrays of results are paginated. `first`, `previous`, `next` and `last` pages are added as `Link` HTTP headers
if needed.

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | The page number
per_page | 100 | The maximum number of results per page
