# User Groups

## List existing User Groups

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const groups = await briq.organization('your-organization').groups();
```

```shell
curl -u briq_api_token "https://api.givebriq.com/v0/organizations/your-organization/groups"
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "ddc1dad7-d323-46d0-97a3-ae806e70e94a",
        "externalRef": null,
        "name": "Team engineering",
        "platform": "briq",
        "created_at": "2018-10-23T13:25:56.670Z",
        "users": [
            {
                "id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
                "role": "user",
                "displayName": "Alice",
                "username": "alice",
                "externalRef": null,
                "email": "alice@your-organization.com",
                "firstName": null,
                "lastName": null,
                "inactiveBalance": 6,
                "activeBalance": 1,
                "platform": "web",
                "image": null,
                "suspended": false,
                "onboardedAt": "2018-10-17T09:55:16.816Z",
                "invitedAt": "2018-10-17T09:54:56.381Z",
                "timezone": "Europe/Brussels",
                "created_at": "2018-10-17T09:55:16.829Z",
            },
            {
                "id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
                "role": "admin",
                "displayName": "Laurent",
                "username": "laurent",
                "externalRef": null,
                "email": "laurent@your-organization.com",
                "firstName": null,
                "lastName": null,
                "inactiveBalance": 5,
                "activeBalance": 0,
                "platform": "web",
                "image": null,
                "suspended": false,
                "onboardedAt": "2018-10-17T09:32:19.722Z",
                "invitedAt": "2018-10-17T09:31:53.883Z",
                "timezone": "Europe/Brussels",
                "created_at": "2018-10-17T09:32:19.736Z",
            }
        ]
    },
]
```

This endpoint lists all the user groups of the organization ([paginated](#pagination))

### HTTP Request

`GET https://api.givebriq.com/v0/organizations/<organization_name>/groups`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization

### Results

This endpoint returns an array of user groups. See [this section](#get-details-of-a-user-group) for a description of a user group.

## Get details of a User Group

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const group = await briq.organization('your-organization').group('group-id');
```

```shell
curl -u briq_api_token "https://api.givebriq.com/v0/organizations/your-organization/groups/group-id"
```

> Replace group-id by the id of the group of which you're getting the details
> The above command returns JSON structured like this:

```json
{
    "id": "ddc1dad7-d323-46d0-97a3-ae806e70e94a",
    "externalRef": null,
    "name": "Team engineering",
    "platform": "briq",
    "created_at": "2018-10-23T13:25:56.670Z",
    "users": [
        {
            "id": "ddfdb19c-e3ad-4300-8ed7-d79e10b9f124",
            "role": "user",
            "displayName": "Alice",
            "username": "alice",
            "externalRef": null,
            "email": "alice@your-organization.com",
            "firstName": null,
            "lastName": null,
            "inactiveBalance": 6,
            "activeBalance": 1,
            "platform": "web",
            "image": null,
            "suspended": false,
            "onboardedAt": "2018-10-17T09:55:16.816Z",
            "invitedAt": "2018-10-17T09:54:56.381Z",
            "timezone": "Europe/Brussels",
            "created_at": "2018-10-17T09:55:16.829Z",
        },
        {
            "id": "eb17a3df-c384-46a9-96a1-d7f58912e19a",
            "role": "admin",
            "displayName": "Laurent",
            "username": "laurent",
            "externalRef": null,
            "email": "laurent@your-organization.com",
            "firstName": null,
            "lastName": null,
            "inactiveBalance": 5,
            "activeBalance": 0,
            "platform": "web",
            "image": null,
            "suspended": false,
            "onboardedAt": "2018-10-17T09:32:19.722Z",
            "invitedAt": "2018-10-17T09:31:53.883Z",
            "timezone": "Europe/Brussels",
            "created_at": "2018-10-17T09:32:19.736Z",
        }
    ]
}
```

This endpoint returns the details for one user groups of the organization.

### HTTP Request

`GET https://api.givebriq.com/v0/organizations/<organization_name>/groups/<group_id>`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization
group_id | The id of the group

### Results

This endpoint returns an object representing a user group, which has the following properties:

Parameter | Description
--------- | -----------
`id` | The id of the group
`name` | The name of the group
`platform` | The platform on which this group was created and is managed (can be `slack` or `briq`)
`externalRef` | If the user group is not a `briq` group, this is the identifier of the group on its original platform
`created_at` | The creation date of the group
`users` | An array of users in the group

