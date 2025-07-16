## Clevertap
**Conversion tracking in CleverTap** is the process of measuring how many users **completed a desired action** — such as a purchase, signup, or feature use — after interacting with a **campaign** or **event funnel**.

### Control Groups
In **CleverTap**, **Control Groups** are used to help you **measure the true effectiveness** of a campaign by comparing it against a **baseline group of users who do not receive the campaign**.

Let’s break this down from **first principles**.

When you run a campaign (push, email, in-app, etc.), users may convert for many reasons:

- They saw your campaign
    
- Or they were going to convert anyway (organic behavior)
    

To **truly measure the campaign's impact**, you need a **control group** — a group of users:

- Who match the campaign audience
    
- But **don’t receive the campaign**
    

This lets you answer:

> _“Did users convert because of the campaign, or would they have anyway?”_


## Limitations of Clevertap
1. 512 events allowed per account (total custom events for us = 512)
2. 256 properties allowed per event
3. maximum of 1000 events records can be send per API call

### Upload Events API
#### [Body Parameters](https://developer.clevertap.com/docs/upload-events-api#body-parameters)

Events are uploaded as a JSON payload. The payload is an object keyed with “d” whose value is an array describing the event including the event name, event properties, timestamp, and user identifier.

Event keys are limited to 120 characters and property values are limited to 512 bytes.

**For each event, a user identifier is required**. This is the key that CleverTap uses to find the user whose profile needs to be updated. You have to set a value for one of these parameters to identify the user: 
1. identity, 
2. FBID, 
3. GPID, or 
4. objectId. *If this identity is not found, a new user profile will be created.*

```json
{
"d" : [
	"Events"
]
}
```

|Parameter|Description|Type|Example Value|
|---|---|---|---|
|type|(Required) Set to event.|string|"event"|
|evtName|(Required) Name of event.|string|“Product Viewed”|
|evtData|(Required) Event properties describing the event. Passed as key/value pairs.|object|"evtData":  <br>{ "Product name": "Casio Watch", "Category": "Mens Watch" }|
|ts|(Optional) Date and time when the event occurred, formatted as a UNIX epoch in seconds. Defaults to the current timestamp if omitted.|ts|1468308340|
|identity|Identity to recognize a unique user. It can be the user’s email, a phone number, or any other identifier you are using to tag your users.  <br>You have to set a value for one of these parameters to identify the user: identity, FBID, GPID, or objectId.|string|“[jack@gmail.com](mailto:jack@gmail.com)”|
|FBID|Identify a unique user by Facebook ID.  <br>  <br>You have to set a value for one of these parameters to identify the user: identity, FBID, GPID, or objectId.|string|“34322423"|
|GPID|Identify a unique user by Google Plus ID.  <br>  <br>You have to set a value for one of these parameters to identify the user: identity, FBID, GPID, or objectId.|string|“34322424"|
|objectId|Identify a unique user by CleverTap Global Object ID.  <br>  <br>You have to set a value for one of these parameters to identify the user: identity, FBID, GPID, or objectId.|string|“34322425"|

Example Payload
```json
{
  "d": [
    {
      "FBID": "34322423",
      "ts": 1468308340,
      "type": "event",
      "evtName": "Product viewed",
      "evtData": {
        "Product name": "Casio Chronograph Watch",
        "Category": "Mens Watch",
        "Price": 59.99,
        "Currency": "USD"
      }
    },
    {
      "identity": "jack@gmail.com",
      "ts": 1468208340,
      "type": "event",
      "evtName": "Charged",
      "evtData": {
        "Amount": 300,
        "Currency": "USD",
        "Payment mode": "Credit Card",
        "Delivery By": "$D_1468322268",
        "Items": [
          {
            "Category": "books",
            "Book name": "The millionaire next door",
            "Quantity": 1
          },
          {
            "Category": "books",
            "Book name": "Achieving inner zen",
            "Quantity": 4
          }
        ]
      }
    }
  ]
}
```

there is no mention of metadata, or expiresAt in the Upload Events API of clevertap

since upload events api is expecting user identity in the payload, so I think we need to search for a more better solution

### External Trigger API
External Trigger campaign is a feature that allows you to trigger the campaign delivery based on API calls or external events.
#### [Base URL](https://developer.clevertap.com/docs/external-trigger-api#base-url)

The base URL varies depending on the type of External Trigger campaign. Here are the example base URLs from the account in the India region:

|Campaign Type|Base URL|
|---|---|
|Single Campaign ID targeting one or more users|[https://in1.api.clevertap.com/1/send/externaltrigger.json](https://in1.api.clevertap.com/1/send/externaltrigger.json)|
|Multiple Campaigns IDs targeting one or more users|[https://in1.api.clevertap.com/2/send/externaltrigger.json](https://in1.api.clevertap.com/2/send/externaltrigger.json)|


### Assumption on the data stored for a user
User interface can be something like this
```typescript
User{
name string;
email string
phoneNumber number;
siteId string; //hahs
}
```
