# Messages

## Create a message

```javascript
const Briq = require('briq-api').Client;
const briq = new Briq('briq_api_token');
const message = await briq.organization('your-organization').createMessage({
  header: 'Alice just earned 3 briqs for outstanding customer service',
  body: '5 ⭐ rating 5 days in a row 🔥',
  channel: '#general'
});
```

WIP