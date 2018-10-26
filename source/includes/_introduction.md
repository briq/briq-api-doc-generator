# Introduction

Welcome to the Briq API.
Briq lets you send Briqs to teammates, small tokens of appreciation to say thanks or congrats.

This API lets you create, read, update and delete (OMG, CRUD) users, user groups, transactions and messages.

We have a [client library in node.js](https://www.github.com/briq/briq-api-node) that will help you craft the perfect requests.

# Authentication

> Use the token to make authenticated calls to the API

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
```

```shell
#Pass the token as the username in a Basic HTTP Authorization header
curl -u briq_api_token: https://www.givebriq.com/v0/organizations/your-organization
```

> Make sure to replace `briq_api_token` with your API key.

Briq uses API tokens to allow access to the API. You can get your token by creating a new custom application in [the Briq admin section](https://www.givebriq.com/app/admin/apps#custom).

Briq only accepts API requests that:

  - use HTTPS
  - include an HTTP Basic Authentication Header using the API token as username and leaving the password blank. 
  
This is supported out of the box by our API client libraires, see [this MDN page](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization#Directives) for manual implementation.
