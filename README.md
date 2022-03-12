# OneSignal NodeJS-Push-Notifications-Sample

<p>
  <a href="https://github.com/OneSignal/onesignal-expo-plugin/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://twitter.com/onesignaldevs" target="_blank">
    <img alt="Twitter: onesignaldevelopers" src="https://img.shields.io/twitter/follow/onesignaldevs?style=social" />
  </a>
</p>

This sample NodeJS app demonstrates how to send push notifications to your app using the OneSignal REST API.

This project was generated with [NodeJS](https://nodejs.org/de/blog/release/v14.16.0/) version v14.16.0

Take a look at the [OneSignal documentation](https://documentation.onesignal.com/docs) to learn how to integrate OneSignal into your project. After you have integrated OneSignal into your application, you can use NodeJS to send push notification using the OneSignal REST API.

## Development server

- Install project dependencie by running `npm i` (npm install).

- Run `npm run start` for a dev server. The app will automatically run the `createNotication()` which will make a call to our API to create a notficationwhich will be sent to your app.

### Options Builder

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

Create a push notification and send it to your users of your app.

- [Postman](https://www.postman.com/onesignaldevs/workspace/onesignal-api/request/16845437-c4f3498f-fd80-4304-a6c1-a3234b923f2c)
- [REST API Reference](https://documentation.onesignal.com/reference#create-notification)

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

View the details from a push notification you have sent using OneSignal.

- [Postman](https://www.postman.com/onesignaldevs/workspace/onesignal-api/request/16845437-6c96ecf0-5882-4eac-a386-0d0cabc8ecd2)
- [REST API Reference](https://documentation.onesignal.com/reference#view-notification)

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

### OneSignal Community

#### Join the OneSignal Developers Community
The OneSignal Developer community is a group of passionate individuals who work with OneSignal products. Community members have the opportunity to expand their network and knowledge across different technologies.

#### TWITTER
Follow our [OneSignal Developers Twitter](https://twitter.com/OneSignalDevs) to learn more about OneSignal, technical tips, and the latest events from OneSignal developers.

#### DISCORD SERVER
The OneSignal Developer community gathers on our public chat server, available on Discord. [Our Discord server](https://discord.gg/EP7gf6Uz7G) is a safe environment to network with other members, ask questions, and learn from each other. It is also a place to engage with the OneSignal product development team.

