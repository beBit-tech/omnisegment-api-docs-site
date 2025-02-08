# Overview

This guide explains how to configure push notifications with deep linking and tracking features in OmniSegment. It covers key setup, content specification, tracking configuration, and manual notification handling on Android. Additionally, a summary and troubleshooting tips are provided for quick reference.


## Settings in OmniSegment

You can embed additional data in your push notifications so that when a user taps a notification, the app can navigate to a specific page or perform a designated action. For example, the notification can direct the user to a particular screen in your app or display a specific image URL.

### Step 1: Key Setup in OmniSegment

Step: Navigate to OmniSegment > Settings > Push Notifications > Key Setup.

Example: Add the following keys into the settings page:
| Key           | Default Value                         |
| ------------- | ------------------------------------- |
| key=action      | name=Action             |
| key=docid | name=Document_ID        |
| key=url       | name=Redirect_URL    |

> [!NOTE]
> The name is an alias used within OmniSegment and does not affect the actual content of the push notification.


<img width="809" alt="截圖 2025-02-08 下午3 00 34" src="https://github.com/user-attachments/assets/956e7417-15cb-45c3-858c-ed432d6f5861" />



### Step.2 Content Specification

> Within the OmniSegment editor, marketing personnel can specify values for the keys (such as action and docid). These values determine the behavior after a push notification is tapped—for example, navigating to a specific app page or executing a particular action.


For FCM (Firebase Cloud Messaging), these custom keys are added to the "data" object in the JSON payload sent to the device.

> [!NOTE]
> Ref：
https://firebase.google.com/docs/cloud-messaging/http-server-ref#downstream-http-messages-json 


FCM Payload Example (Android):
```json
{
  "registration_ids": ["1", "2", "3", ...],
  "data": {
    "title": "TITLE",
    "body": "BODY",
    "action": "popup",
    "docid": "123",
    ...
  }
}
```

FCM Payload Example (iOS):
```json
{
  "registration_ids": ["1", "2", "3", ...],
  "data": {
    "action": "popup",
    "docid": "123",
    ...
  },
  "notification": {
    "title": "TITLE",
    "body": "BODY",
  }
}
```

***
# App Push Tracking Guide

## Use Case

* Use the [Event Tracking API](https://github.com/beBit-tech/omnisegment-api-docs/wiki/Event-Tracking-API) to monitor app performance.
* Use the [APP SDK](https://github.com/beBit-tech/bebit-tech-ios-app-sdk/wiki/Track-events) to record user interactions and events.

## Variables

* `destination_url`: The base URL used to generate the omnisegment_tracking_url. It indicates the link you want to track.
* `omnisegment_tracking_url`: This URL is included in the push notification’s data payload (as a [DataMessage](https://firebase.google.com/docs/cloud-messaging/concept-options) ). It tracks the interaction between the push and the user’s subsequent actions.
* `document_location`: The page key or page URL, referred to as [location](https://github.com/beBit-tech/bebit-tech-ios-app-sdk/wiki/Track-events#event-properties) in the SDK.
* variable sample
```
destination_url: https://shop/product/123
omnisegment_tracking_url:  https://omnsegment.com/collect?v=1&t=event&dr=pn&tid=oa-319523&ea=TrackingClick&ec=Tracking&luid=35431545_135123125&tuid=1231412351_13251232_3412351
document_location: https://shop/product/123?omniclid=1325123_1251932&utm_id=omnisegment
```


## How to

* Pre-Setup in the OS System

1. In OmniSegment > Settings > Push Notifications > Key Setup, add the key destination_url.
2. In the OmniSegment push notification template editor, add the corresponding destination_url value.

*  APP Handling After a Push Notification Tap

1.  Initial Request:
    - (a)After the user taps the push notification, the app should send a GET request using the omnisegment_tracking_url. The response should return a 302 Redirect to the document_location.
    - (b) If the redirect location cannot be obtained properly as described in (1.a), replace the parameter goto=1 with goto=0 in the omnisegment_tracking_url, send a GET request, and the response will return 200_OK along with the document_location.
2.  Navigation and Tracking:
    - Once the document_location is retrieved, update the app’s page parameters and send the corresponding tracking event (using trackEvent).

## Example: Retrieve Document Location

if you want to only get document location, you can add `goto=0` and then the response text will be the document location

```javascript
  const getDocumentLocation = async (tracking_url) => {
    try {
      const response = await fetch(`${tracking_url}&goto=0`);
      const text = await response.text();
      console.log(text);
    } catch (error) {
      console.error("Failed to fetch data:", error);
    }
  };

```
## Example: Handling Notification Tap in React Native
```javascript
import RNFetchBlob from 'rn-fetch-blob';


 private _didTapNotificationBannerAndOpenApp(props: {notification: Notification, completion: () => void}) {
        const payload = props.notification.payload

        const tracking_url = props.notification.payload?.omnisegment_tracking_url
        if (tracking_url) {
               RNFetchBlob.config({
                // Configuration options
              })
              .fetch('GET', tracking_url)
              .then((res) => {
                if (res.info().status === 200) {

                  // EXPECT DOCUMENT LOCATION URL will have omniclid in params
                  console.log('document location here: ', res.respInfo.redirects[1]);

                 }
                }
              })
              .catch((error) => {
                // Handle error
                console.log('Redirected error:', error);

              });

        }

        console.log(
            `Opne App for Notification payload: ` +
            JSON.stringify(props) 
        )

        props.completion()
    }
```

## Manually handle notification on android

Since we only send data messages to Android devices, you must manually display the notification.


### React Native Example

```js
import PushNotification from "react-native-push-notification";

PushNotification.localNotification({
  channelId: "android.bebit.newmessage", // Make sure to create this channel on Android
  title: notification.payload.title, // The title of the notification
  message: notification.payload.body,
  playSound: true, // Sound
  soundName: "default", // Play the default sound
  importance: "high", // Android only
  priority: "high", // Android only
});
```
