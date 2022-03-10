# OneSignal NodeJS-Push-Notifications-Sample

This sample NodeJS app demonstrates how to send push notifications to your app using the OneSignal REST API.

This project was generated with [NodeJS](https://nodejs.org/de/blog/release/v14.16.0/) version v14.16.0

## Development server

- Install project dependencie by running `npm i` (npm install).

- Run `npm run start` for a dev server. The app will automatically run the `createNotication()` which will make a call to our API to create a notficationwhich will be sent to your app.

### OptionsBuilder

This function generated an options object containing the information need it to make the API call. Below you can find a sample object generated after running the `optionsBuilder(method, path, body)` function. This function was created for reusability purposes, no need to have this function to run the OneSignal REST API, all you need is an options object.

```javascript
{
    method: 'POST',
    url: 'https://onesignal.com/api/v1/notifications',
    headers: {
        'Content-Type': 'application/json',
        Authorization: 'Basic API_KEY'
    },
    body: {
      app_id:'API_ID',
      included_segments:['Subscribed Users'],
      data:{foo:'bar'},
      contents:{en:'Sample Push Message'}
    }
}
```

### Create Notification
```javascript
const createNotication = (body) => {
    const options = optionsBuilder("POST","notifications", body);
    request(options, (error, response) => {
        if (error) throw new Error(error);
        console.log(response.body);
        viewNotifcation(JSON.parse(response.body).id);
    });
}
```
### View Notification

View the details from a push notification you have sent using OneSignal

```javascript
const viewNotifcation = (notificationId) => {

    const path = `notifications/${notificationId}?app_id=${ONE_SIGNAL_APP_ID}`;
    const options = optionsBuilder("GET", path);
    request(options, (error, response)=> {
        if (error) throw new Error(error);
        console.log(response.body);
    });
}
```