# Organization

## Get details of your organization

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const organization = await briq.organization('your-organization').info();
```

```shell
curl -u briq_api_token "https://api.givebriq.com/v0/organizations/your-organization"
```

> Replace `your-organization` with the name of your organization (find it in [your Briq settings](https://www.givebriq.com/app/admin/)).
> The above command will resolve to a JSON structured like this:

```json
{
    "id": "c5e91a81-0c92-4069-b002-26e8df8aa556",
    "key": "your-organization",
    "created_at": "2018-10-17T09:31:27.907Z"
}
```

This endpoint retrieves information about the current organization.

### HTTP Request

`GET https://api.givebriq.com/v0/organizations/<organization_name>`

### URL Parameters

Parameter | Description
--------- | -----------
organization_name | The name of your organization
