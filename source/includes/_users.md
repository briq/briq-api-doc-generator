# Users

## List all users of organization

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const users = await briq.organization('your-organization').users();
```

```shell
curl -u briq_api_token "https://www.givebriq.com/v0/organizations/your-organization/users"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
    "username": "alice@your-organization.com",
    "displayName": "Alice",
    "email": "alice@your-organization.com",
    "externalRef": null,
    "firstName": null,
    "lastName": null,
    "inactiveBalance": 6,
    "activeBalance": 1,
    "role": "user",
    "created_at": "2018-10-17T09:55:16.829Z",
    "image": null
  },
  {
    "id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
    "username": "laurent@your-organization.com",
    "displayName": "Laurent",
    "email": "laurent@your-organization.com",
    "externalRef": null,
    "firstName": null,
    "lastName": null,
    "inactiveBalance": 5,
    "activeBalance": 0,
    "role": "admin",
    "created_at": "2018-10-17T09:32:19.736Z",
    "image": null
  }
]
```

This endpoint lists all the users of the organization ([paginated](#pagination)).

### HTTP Request

`GET https://www.givebriq.com/v0/organizations/<organization_name>/users`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization

### Results

This endpoint returns an array of users. See [this section](#get-details-of-a-user) for a description of a user.

## Get details of a user

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const user = await briq.organization('your-organization').user('user-id');
```

```shell
curl -u briq_api_token "https://www.givebriq.com/v0/organizations/your-organization/users/user-id"
```

> Replace `user-id` with the id of the user
> The above command returns JSON structured like this:

```json
{
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
```

This endpoint retrieves the details of a user.

### HTTP Request

`GET https://www.givebriq.com/v0/organizations/<organization_name>/users/<user_id>`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization
user_id | The id of the user to fetch (`username` and `externalRef` can be used too)

### Results

This endpoint returns a JSON user with the following attributes:

Parameter | Description
--------- | -----------
`id` | The unique identifier of the user
`username` | The username of the user, must be unique per organization
`email` | The email of the user, must be unique per organization
`displayName` | The name to use for the user in the interface,
`externalRef` | A string referencing the user in another data source
`firstName` | The first name of the user
`lastName` | The last name of the user
`inactiveBalance` | The balance of Briqs to give
`activeBalance` | The balance of Briqs to redeem
`role` | The role of the user (values: `user`, `admin`)
`image` | A URL for an image to be used as avatar for the user
`created_at` | The timestamp at which this user was created
`invitedAt` | The timestamp at which this user was invited to participate to Briq
`onboardedAt` | The timestamp at which this user completed their onboarding
`timezone` | The timezone configured for this user
`platform` | The plaform from which this user was created (can be `slack` or  `web`)
`suspended` | A flag that is `true` if the user has been suspended
