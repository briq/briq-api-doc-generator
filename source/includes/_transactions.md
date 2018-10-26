# Transactions

## List transactions

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const transactions = await briq.organization('your-organization').transactions();
```

```shell
curl -u briq_api_token "https://www.givebriq.com/v0/organizations/your-organization/transactions"
```

> The above command returns JSON structured like this:

```json
[
        {
        "id": "8f49eb2e-2184-4966-be36-9a86db95bd0d",
        "from": "Laurent",
        "to": "Alice",
        "amount": 1,
        "comment": "Hello Alice  #TeamSpirit #Teamwork",
        "app": "give",
        "created_at": "2018-10-18T08:54:02.853Z",
        "reaction": null,
        "reactedAt": null,
        "user_from_id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
        "user_to_id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124"
    }
]
```

This endpoint lists all the transactions of the organization ([paginated](#pagination))

### HTTP Request

`GET https://www.givebriq.com/v0/organizations/<organization_name>/transactions`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization

### Results

This endpoint returns an array of transactions. See [this section](#get-details-of-a-transaction) for a description of a transaction.

## Get details of a transaction

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const transaction = await briq.organization('your-organization').transaction('transaction-id');
```

```shell
curl -u briq_api_token "https://www.givebriq.com/v0/organizations/your-organization/transactions/transaction-id"
```

> Replace `transaction-id` with the id of the transaction
> The above command returns JSON structured like this:

```json
{
    "id": "8f49eb2e-2184-4966-be36-9a86db95bd0d",
    "from": "Laurent",
    "to": "Alice",
    "amount": 1,
    "comment": "Hello Alice  #TeamSpirit #Teamwork",
    "app": "give",
    "created_at": "2018-10-18T08:54:02.853Z",
    "reaction": null,
    "reactedAt": null,
    "user_from_id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
    "user_to_id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
    "userFrom": {
        "id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
        "username": "laurent",
        "displayName": "Laurent",
        "email": "laurent@your-organization.com",
        "externalRef": null,
        "firstName": null,
        "lastName": null,
        "inactiveBalance": 5,
        "activeBalance": 0,
        "role": "admin",
        "created_at": "2018-10-17T09:32:19.736Z",
        "image": null,
        "invitedAt": "2018-10-17T09:31:53.883Z",
        "onboardedAt": "2018-10-17T09:32:19.722Z",
        "timezone": "Europe/Brussels",
        "platform": "web",
        "suspended": false
    },
    "userTo": {
        "id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
        "username": "alice",
        "displayName": "Alice",
        "email": "alice@your-organization.com",
        "externalRef": null,
        "firstName": null,
        "lastName": null,
        "inactiveBalance": 6,
        "activeBalance": 1,
        "role": "user",
        "created_at": "2018-10-17T09:55:16.829Z",
        "image": null,
        "invitedAt": "2018-10-17T09:54:56.381Z",
        "onboardedAt": "2018-10-17T09:55:16.816Z",
        "timezone": "Europe/Brussels",
        "platform": "web",
        "suspended": false
    }
}
```

This endpoint retrieves the details of a transaction.

### HTTP Request

`GET https://www.givebriq.com/v0/organizations/<organization_name>/transactions/<transaction_id>`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization
transaction_id | The id of the transaction to fetch

### Results

This endpoint returns a JSON transaction with the following attributes:

Parameter | Description
--------- | -----------
`id` | The unique identifier of the transaction
`from` | The name of the user who gave Briqs for this transaction
`to` | The name of the user who received Briqs for this transaction
`amount` | The number of Briqs moved by the transaction
`comment` | The comment on the transaction (usually the reason for the give to take place)
`app` | The name of the app that created the transaction
`created_at` | The creation date of the transaction
`reaction` | The reaction that has been added to the transaction
`reactedAt` | The timestamp when the reaction was added
`user_from_id` | The id of the user who gave Briqs
`user_to_id` | The id of the user who received Briqs
`userFrom` | The user who gave Briqs, as a JSON object (see [this section](#get-details-of-a-user) for details)
`userTo` | The user who received Briqs, as a JSON object (see [this section](#get-details-of-a-user) for details)

## Create a transaction

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const transaction = await briq.organization('your-organization').createTransaction({
  amount: 2,
  comment: 'Thanks for your help with the presentation #teamspirit',
  from: 'alice',
  to: 'laurent'
});
```

```shell
curl -i -u briq_api_token
  --header "Content-Type: application/json" \
  --request POST \
  --data '{ "amount": 2, "comment": "Thanks for your help with the presentation #teamspirit", "from": "alice", "to": "laurent" }' \
  "https://www.givebriq.com/v0/organizations/your-organization/transactions"
```

> The above command returns an HTTP `201 Created` response and includes a `Location` header with the URL of the created transaction.
> It also includes the created transaction as JSON in the response

```
{
    "id": "e9758206-8f81-4292-a225-c4e7dab25cf8",
    "from": "Alice",
    "to": "Laurent",
    "amount": 1,
    "comment": "Thanks for your help with the presentation #teamspirit",
    "app": "API Documentation",
    "created_at": "2018-10-25T14:47:40.597Z",
    "reaction": null,
    "reactedAt": null,
    "user_from_id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
    "user_to_id": "eb17a3df-c384-46a9-96a1-d7f58912e19a"
}
```

This endpoint creates a transaction.

### HTTP Request

`POST https://www.givebriq.com/v0/organizations/<organization_name>/transactions`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization

### Body

A transaction can be created with the following attributes

Parameter | Description
--------- | -----------
`from` | The `id`, `username`, `email` or `externalRef` of the user who gave Briqs for this transaction. It can be empty, meaning that the user `to` will receive Briqs from the bank
`to` | The `id`, `username`, `email` or `externalRef` of the user who receives Briqs for this transaction. It can be empty, meaning that the user `from` will spend Briqs from their active balance (redemption)
`amount` | The number of Briqs moved by the transaction
`comment` | The comment on the transaction (usually the reason for giving/redeeming briqs)

### Results

The created transaction is returned as JSON in the body of the response. See [this section](#get-details-of-a-transaction) for more details

## Revert a transaction

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const transaction = await briq.organization('your-organization').refundTransaction('transaction-id');
```

```shell
curl -i -u briq_api_token --request DELETE "https://www.givebriq.com/v0/organizations/your-organization/transactions/transaction-id"
```

> Replace `transaction-id` with the id of the transaction
> The above command returns an HTTP `204 No Content` and an empty body when the revert is successful

This endpoint reverts a transaction.

### HTTP Request

`DELETE https://www.givebriq.com/v0/organizations/<organization_name>/transactions/<transaction_id>`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization
transaction_id | The id of the transaction to revert

### Results

If the revert is successful, an HTTP `204 No content` response is sent.