This below request is coming alright
1. With DeviceId
```json
**c5url** -X POST "https://api.clevertap.com/1/send/push.json" \
-H "X-CleverTap-Account-Id: 449-R46-R57Z" \
-H "X-CleverTap-Passcode: AAS-IAY-MPEL" \
-H "Content-Type: application/json; charset=utf-8" \
-d '{
  "to": {
    "objectId": [
      "-vd4c1f82c048c49e6ba9ab611de4aa4c7"
    ]
  },
  "content": {
    "title": "Hey Device Homer",
    "body": "This is a test push notification with image and custom params.",
    "platform_specific": {
      "android": {
        "large_icon": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
        "wzrk_cid": "vdp_ring_channel_id",
        "background_image": "https://utsav.gov.in/public/festival_top/1659608853.jpg"
      },
      "ios": {
        "sound_file": "ring_sound.wav",
        "mutable-content": "true",
        "ct_mediaUrl": "https://i0.wp.com/www.dogwonder.co.uk/wp-content/uploads/2009/12/tumblr_ku2pvuJkJG1qz9qooo1_r1_400.gif?resize=320%2C320"
      }
    },
    "params": {
      "foo": "bar",
      "baz": 123
    }
  }
}'

```

2. with userId
```json
curl -X POST "https://api.clevertap.com/1/send/push.json" \
-H "X-CleverTap-Account-Id: 449-R46-R57Z" \
-H "X-CleverTap-Passcode: AAS-IAY-MPEL" \
-H "Content-Type: application/json; charset=utf-8" \
-d '{
  "to": {
    "Identity": [
    "+918247781785",
    ]
  },
  "content": {
    "title": "Hey User Identity Homer",
    "body": "This is a test push notification with image and custom params.",
    "platform_specific": {
      "android": {
        "large_icon": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
        "wzrk_cid": "vdp_ring_channel_id",
        "background_image": "https://utsav.gov.in/public/festival_top/1659608853.jpg"
      },
      "ios": {
        "sound_file": "ring_sound.wav",
        "mutable-content": "true",
        "ct_mediaUrl": "https://i0.wp.com/www.dogwonder.co.uk/wp-content/uploads/2009/12/tumblr_ku2pvuJkJG1qz9qooo1_r1_400.gif?resize=320%2C320"
      }
    },
    "params": {
      "foo": "bar",
      "baz": 123
    }
  }
}'
```
## Carousel example
```json
curl -X POST "https://api.clevertap.com/1/send/push.json" \
-H "X-CleverTap-Account-Id: 449-R46-R57Z" \
-H "X-CleverTap-Passcode: AAS-IAY-MPEL" \
-H "Content-Type: application/json; charset=utf-8" \
-d '{
  "to": {
    "objectId": [
      "-vd4c1f82c048c49e6ba9ab611de4aa4c7"
    ]
  },
  "content": {
    "title": "Hey Man",
    "body": "This is a test push notification with image and custom params.",
    "platform_specific": {
      "android": {
        "large_icon": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
        "wzrk_cid": "vdp_ring_channel_id",
        "background_image": "https://utsav.gov.in/public/festival_top/1659608853.jpg"
      },
      "ios": {
		    "sound_file": "cutoms_sound.wac"
			"mutable-content": "true", 
			"ct_mediaUrl": "https://static.vecteezy.com/system/resources/thumbnails/057/068/323/small/single-fresh-red-strawberry-on-table-green-background-food-fruit-sweet-macro-juicy-plant-image-photo.jpg",
            },
    },
    "params": "{\"foo\":\"bar\",\"baz\":123}"
  }
}'

```



Shield Request
```json
curl --location 'http://100.96.62.107:3939/api/v1/notification/send_clevertap_notification' \
--header 'Content-Type: application/json' \
--data '[
  {
    "time": "2025-10-09T12:37:15Z",
    "msg": "Notification request for user-123",
    "data": {
      "notification": {
        "eventId": "a7e1c8b3-9f8e-4b1d-8c2a-5e7d6f0b1a2c",
        "source": "appliance-monitor-service",
        "channel": "PUSH",
        "target": {
          "clevertap_device_id": [
            "__ac8bfb751f384373878f9004e3f6f10a",
            "-vd4c1f82c048c49e6ba9ab611de4aa4c7"
          ]
        },
        "payload": {
          "title": "Appliance Alert! 5",
          "body": "Your device in floor12 requires attention.",
          "imageUrl": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
          "soundFile": "ring_sound.wav",
          "channelId": "vdp_ring_channel_id",
          "locale": "en",
          "deepLink": "myapp://appliance/kdjkji2",
          "params": {
            "applianceId": "kdjkji2",
            "room": "floor12",
            "alertCode": "TEMP_HIGH"
          }
        },
        "delivery": {
          "priority": "HIGH",
          "ttl": 86400
        }
      }
    }
  }
]'

```


using shield domain

> [!WARN]
> Always update the zulu time with current time

```json
curl --location 'https://shield.dev.keus.in/api/v1/notification/send_clevertap_notification' \
--header 'Content-Type: application/json' \
--data '[
  {
    "time": "2025-10-15T09:33:09Z",
    "msg": "Notification request for user-123",
    "data": {
      "notification": {
        "eventId": "a7e1c8b3-9f8e-4b1d-8c2a-5e7d6f0b1a2c",
        "source": "appliance-monitor-service",
        "channel": "PUSH",
        "target": {
          "clevertap_device_id": [
            "__ac8bfb751f384373878f9004e3f6f10a",
            "-vd4c1f82c048c49e6ba9ab611de4aa4c7"
          ]
        },
        "payload": {
          "title": "Appliance Alert! 5",
          "body": "Your device in floor12 requires attention.",
          "imageUrl": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
          "soundFile": "ring_sound.wav",
          "channelId": "vdp_ring_channel_id",
          "locale": "en",
          "deepLink": "myapp://appliance/kdjkji2",
          "params": {
            "applianceId": "kdjkji2",
            "room": "floor12",
            "alertCode": "TEMP_HIGH"
          }
        },
        "delivery": {
          "priority": "HIGH",
          "ttl": 8640000
        }
      }
    }
  }
]'

```

using userId
```json
curl --location 'https://shield.dev.keus.in/api/v1/notification/send_clevertap_notification' \
--header 'Content-Type: application/json' \
--data '[
  {
    "time": "2025-10-17T12:04:22Z",
    "msg": "Notification request for user-123",
    "data": {
      "notification": {
        "eventId": "a7e1c8b3-9f8e-4b1d-8c2a-5e7d6f0b1a2c",
        "source": "appliance-monitor-service",
        "channel": "PUSH",
        "target": {
          "userId": "+918247781785"
        },
        "payload": {
          "title": "Appliance Alert! 5",
          "body": "Your device in floor12 requires attention.",
          "imageUrl": "https://utsav.gov.in/public/festival_top/1659608853.jpg",
          "soundFile": "ring_sound.wav",
          "channelId": "vdp_ring_channel_id",
          "locale": "en",
          "deepLink": "myapp://appliance/kdjkji2",
          "params": {
            "applianceId": "kdjkji2",
            "room": "floor12",
            "alertCode": "TEMP_HIGH"
          }
        },
        "delivery": {
          "priority": "HIGH",
          "ttl": 86400
        }
      }
    }
  }
]'
```


Sample
```json
curl --location 'https://shield.dev.keus.in/api/v1/notification/send_clevertap_notification' \
--header 'Content-Type: application/json' \
--data '[
  {
    "time": "2025-10-17T12:04:22Z",
    "msg": "Notification request for user-123",
    "data": {
      "notification": {
      "eventId": "KIOTP-NOTIFICATION-camera",
      "channel": "PUSH",
      "target": {
        "userId": "+918247781785"
      },
      "payload": {
        "title": "Camera Detection",
        "body": "Motion Detected in camera null",
        "locale": "en",
        "soundFile": "ring_sound.wav",
        "imageUrl": "https://i0.wp.com/www.dogwonder.co.uk/wp-content/uploads/2009/12/tumblr_ku2pvuJkJG1qz9qooo1_r1_400.gif?resize=320%2C320",
        "params": {
          "applianceId": "68e7a7d5fc5d4fd32b055add",
          "applianceName": "",
          "eventId": "68f22f5b0086ca03e41a802e",
          "eventStartTime": 1760702293755,
          "eventEndTime": 1760702301755,
          "eventThumbnailId": "https://heimdall.keus.in/708bc8980000000000000000-kiotp.plugins.cameras.core/snapshot/672dc2b60006a603e400121d",
          "detectionType": 2
        }
      },
        "delivery": {
          "priority": "HIGH",
          "ttl": 86400
        }
      }
    }
  }
]'
```