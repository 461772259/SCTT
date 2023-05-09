## Getting started

1. open app_V2.exe
```
接口已启动
```

2. Create your first chat connection：Use websocket to connect to local port 3000, for example: 127.0.0.1:3000, and send "platform code@live room number"
```
Unity c# code example：

this.socketIo = new WebSocket("ws://127.0.0.1:3000", Array.Empty<string>());
		this.socketIo.OnMessage += delegate(object o, MessageEventArgs e)
		{
			//TODO
		};
		this.socketIo.OnError += delegate(object sender, ErrorEventArgs e)
		{
			Debug.Log(levelName+ "： socket Error: " + e.Message.ToString());
		};
		this.socketIo.Connect();
		this.socketIo.Send("{platform code}@{live room code}"); //eg:Shanggu@maizi869
```

3. parsing message

```
message的格式为："{event}\0{data}"
eg: chat{"comment":"6","userId":"6506646277295882242","secUid":"MS4wLjABAAAA6072z27Df6gadz_jKprf5Ozi8H0U6l5etANktpImf2tQ7KDl6HCesEe6-9PEhgNP","uniqueId":"gu12246","nickname":"Shîñ","profilePictureUrl":"https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/388b20bd690fec33398dab2944751312~c5_100x100.webp?x-expires=1683817200&x-signature=kvpbch5FNMbQjmdjUk8wWJSrnmg%3D","followRole":1,"userBadges":[{"type":"image","badgeSceneType":6,"displayType":1,"url":"https://p19-webcast.tiktokcdn.com/webcast-sg/new_top_gifter_version_2.png~tplv-obj.image"}],"userDetails":{"createTime":"0","bioDescription":"","profilePictureUrls":["https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/388b20bd690fec33398dab2944751312~tplv-tiktok-shrink:72:72.webp?x-expires=1683817200&x-signature=GYAPGZwly9d9BhINmlpGXF6ugUA%3D","https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/388b20bd690fec33398dab2944751312~c5_100x100.webp?x-expires=1683817200&x-signature=kvpbch5FNMbQjmdjUk8wWJSrnmg%3D","https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/388b20bd690fec33398dab2944751312~c5_100x100.jpeg?x-expires=1683817200&x-signature=nVYCv%2Bpm6svGqtAGn7glD6VUgNA%3D"]},"followInfo":{"followingCount":888,"followerCount":803,"followStatus":1,"pushStatus":0},"isModerator":false,"isNewGifter":false,"isSubscriber":false,"topGifterRank":null,"msgId":"7231207847282658053","createTime":"1683646785594"}
```

## Events

Message Events:
- [member](#member)
- [chat](#chat)
- [gift](#gift)
- [roomUser](#roomuser)
- [like](#like)
- [social](#social)
- [emote](#emote)
- [envelope](#envelope)
- [questionNew](#questionnew)
- [linkMicBattle](#linkmicbattle)
- [linkMicArmies](#linkmicarmies)
- [liveIntro](#liveintro)
- [subscribe](#subscribe)

Custom Events:
- [follow](#follow)
- [share](#share)

<br><br>

### Message Events

### `member`
Triggered every time a new viewer joins the live stream.

```
member\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    actionId: 1,
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends
    userBadges: [
        {
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...jpeg"
        ]
    },
    followInfo: {
        followingCount: 2139,
        followerCount: 853,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750885996120859",
    createTime: "1661887134195",
    displayType: "live_room_enter_toast",
    label: "{0:user} joined"
}
```
</p></details>

<br>

### `chat`
Triggered every time a new chat comment arrives.

```
chat\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    comment: "How are you?",
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends
    userBadges: [
        {
            // Moderator badge
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            // Top Gifter badge
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            // Subscriber Badge
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...jpeg"
        ]
    },
    followInfo: {
        followingCount: 10000,
        followerCount: 606,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750790064065286",
    createTime: "1661887134718"
}
```
</p></details>
<br>

### `gift`
Triggered every time a gift arrives. You will receive additional information via the `extendedGiftInfo` attribute when you enable the [`enableExtendedGiftInfo`](#params-and-options) option. 

> **NOTE:** Users have the capability to send gifts in a streak. This increases the `repeatCount` value until the user terminates the streak. During this time new gift events are triggered again and again with an increased `repeatCount` value. It should be noted that after the end of the streak, another gift event is triggered, which signals the end of the streak via `repeatEnd`:`true`. This applies only to gifts with `giftType`:`1`. This means that even if the user sends a `giftType`:`1` gift only once, you will receive the event twice. Once with `repeatEnd`:`false` and once with `repeatEnd`:`true`. Therefore, the event should be handled as follows:


```javascript
gift\0{data}
```


<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    // Gift Details
    giftId: 5953,
    repeatCount: 1,
    repeatEnd: true,
    groupId: "1661887131074",
    monitorExtra: {
        anchor_id: 7087613897129494000,
        from_idc: "maliva",
        from_user_id: 7044640112358049000,
        gift_id: 5953,
        gift_type: 1,
        log_id: "20220830191849010192055159174B7670",
        msg_id: 7137749190944230000,
        repeat_count: 1,
        repeat_end: 1,
        room_id: 7137728632142843000,
        send_gift_profit_core_start_ms: 0,
        send_gift_send_message_success_ms: 1661887134397,
        to_user_id: 7087613897129494000
    },
    // Sender Details
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...jpeg"
        ]
    },
    followInfo: {
        followingCount: 360,
        followerCount: 740,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137749190944230150",
    createTime: "1661887134397",
    displayType: "webcast_aweme_gift_send_message",
    label: "{0:user} sent {1:gift} {2:string}",
    gift: {
        gift_id: 5953,
        repeat_count: 1,
        repeat_end: 1,
        gift_type: 1
    },
    describe: "Sent Nevalyashka doll",
    giftType: 1,
    diamondCount: 25,
    giftName: "Nevalyashka doll",
    giftPictureUrl: "https://p19-webcast.tiktokcdn.com/img/maliva/webca...png",
    timestamp: 1661887134397,
    extendedGiftInfo: {
        // This will be filled when you enable the `enableExtendedGiftInfo` option
    },

    // Receiver Details (can also be a guest broadcaster)
    receiverUserId: "7087613897129493510"
}
```
</p></details>
<br>

### `roomUser`
Triggered every time a statistic message arrives. This message currently contains the viewer count and a top gifter list.

```javascript
roomUser\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    topViewers: [
        {
            user: {
                userId: "6822565897317303297",
                secUid: "MS4wLjABAAAALIKFhzvmiCws6B6KWfRgWr5MbyGVPXevakvnP8xc7VLkWtcqNeEe9coyRA74KNxm",
                uniqueId: "linmjh",
                nickname: "gì z má ( ^ㆍㅅㆍ^)",
                profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
                followRole: 0,
                userBadges: [],
                userDetails: {
                    createTime: "1588502711",
                    bioDescription: "",
                    profilePictureUrls: [
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
                        "https://p9-sign-sg.tiktokcdn.com/aweme/100x100/tos...webp",
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...jpeg"
                    ]
                },
                followInfo: {
                    followingCount: 781,
                    followerCount: 51,
                    followStatus: 0,
                    pushStatus: 0
                },
                isModerator: false,
                isNewGifter: false,
                isSubscriber: false,
                topGifterRank: null
            },
            coinCount: 0
        },
        {
            user: {
                userId: "6828542044454863874",
                secUid: "MS4wLjABAAAAxP4NgzG7uJz1tcB8o3JN8PxHWej20NJWCHP1IG1PZ0OmQLB6SVORRSoX0Ool4dwj",
                uniqueId: "xuanthainguyen0",
                nickname: "Xuan Thai Nguyen",
                profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...webp",
                followRole: 0,
                userBadges: [],
                userDetails: {
                    createTime: "1593865836",
                    bioDescription: "",
                    profilePictureUrls: [
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...webp",
                        "https://p9-sign-sg.tiktokcdn.com/aweme/100x100/tik...webp",
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...jpeg"
                    ]
                },
                followInfo: {
                    followingCount: 6,
                    followerCount: 6,
                    followStatus: 0,
                    pushStatus: 0
                },
                isModerator: false,
                isNewGifter: false,
                isSubscriber: false,
                topGifterRank: null
            },
            coinCount: 0
        },
        {
            user: {
                userId: "7014684709204624385",
                secUid: "MS4wLjABAAAAnVMJ9MXN5HqjnpyEwgEhjv97Pc_ixtG4Iwnnagbrd99WhEATfhZLW6McX-uErTp9",
                uniqueId: "dyip0c3sbo2t",
                nickname: "Huu Trân572",
                profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...webp",
                followRole: 0,
                userBadges: [],
                userDetails: {
                    createTime: "1640318249",
                    bioDescription: "",
                    profilePictureUrls: [
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...webp",
                        "https://p9-sign-sg.tiktokcdn.com/aweme/100x100/tik...webp",
                        "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/ti...jpeg"
                    ]
                },
                followInfo: {
                    followingCount: 35,
                    followerCount: 21,
                    followStatus: 0,
                    pushStatus: 0
                },
                isModerator: false,
                isNewGifter: false,
                isSubscriber: false,
                topGifterRank: null
            },
            coinCount: 0
        },
        {
            user: {
                userId: "7133413217468187675",
                secUid: "MS4wLjABAAAA2u64n6KnroBOMQo4pR9bLv0twyCIy0X-wd7S__WR4d2VObktWAfs_ck08pjD4hIV",
                uniqueId: "uservay64gw9d5",
                nickname: "uservay64gw9d5",
                profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
                followRole: 0,
                userBadges: [],
                userDetails: {
                    createTime: "1660877330",
                    bioDescription: "",
                    profilePictureUrls: [
                        "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
                        "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...jpeg"
                    ]
                },
                followInfo: {
                    followingCount: 2,
                    followerCount: 0,
                    followStatus: 0,
                    pushStatus: 0
                },
                isModerator: false,
                isNewGifter: false,
                isSubscriber: false,
                topGifterRank: null
            },
            coinCount: 0
        },
        {
            user: {
                userId: "6800374961430791170",
                secUid: "MS4wLjABAAAAF3tD_kSi9qas_10I5I5YUIBfXKd0KlKvKTKACzfXS1Wwp04e03xJCTswwzCMRgEu",
                uniqueId: "hungtran0293",
                nickname: "Trần Hùng",
                profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
                followRole: 0,
                userBadges: [],
                userDetails: {
                    createTime: "1585370455",
                    bioDescription: "",
                    profilePictureUrls: [
                        "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...webp",
                        "https://p16-sign-va.tiktokcdn.com/tos-useast2a-avt...jpeg"
                    ]
                },
                followInfo: {
                    followingCount: 1735,
                    followerCount: 313,
                    followStatus: 0,
                    pushStatus: 0
                },
                isModerator: false,
                isNewGifter: false,
                isSubscriber: false,
                topGifterRank: null
            },
            coinCount: 0
        }
    ],
    viewerCount: 630
}
```
</p></details>

<br>

### `like`
Triggered when a viewer sends likes to the streamer. For streams with many viewers, this event is not always triggered by TikTok.

```javascript
like\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    likeCount: 6, // likes given by the user (taps on screen)
    totalLikeCount: 21349, // likes that this stream has received in total (from all users)
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends,
    userBadges: [
        {
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p19-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...jpeg"
        ]
    },
    followInfo: {
        followingCount: 617,
        followerCount: 112,
        followStatus: 1,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750883651619630",
    createTime: "1661887134554",
    displayType: "pm_mt_msg_viewer",
    label: "{0:user} liked the LIVE"
}
```
</p></details>
<br>

### `social`
Triggered every time someone shares the stream or follows the host.

```javascript
social\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
    followRole: 1,
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p19-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...jpeg"
        ]
    },
    followInfo: {
        followingCount: 277,
        followerCount: 96,
        followStatus: 1,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750889884076842",
    createTime: "1661887134629",
    displayType: "pm_main_follow_message_viewer_2", // or pm_mt_guidance_share
    label: "{0:user} followed the host"
}
```
</p></details>
<br>

### `emote`
Triggered every time a subscriber sends an emote (sticker).

```javascript
emote\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends,
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-sg.tiktokcdn.com/tos-alisg-avt-00...webp",
            "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
            "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...jpeg"
        ]
    },
    followInfo: {
        followingCount: 14,
        followerCount: 6,
        followStatus: 1,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: true,
    topGifterRank: null,
    emoteId: "7121025198379731714",
    emoteImageUrl: "https://p19-webcast.tiktokcdn.com/webcast-sg/61964...image"
}
```
</p></details>
<br>

### `envelope`
Triggered every time someone sends a treasure chest.

```javascript
envelope\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-webcast.tiktokcdn.com/img/alisg/webcas...png",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-webcast.tiktokcdn.com/img/alisg/webcas...png",
            "https://p19-webcast.tiktokcdn.com/img/alisg/webcas...png"
        ]
    },
    followInfo: {
        followingCount: 828,
        followerCount: 1353,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    coins: 20,
    canOpen: 20,
    timestamp: 1661887422
}
```
</p></details>
<br>

### `questionNew`
Triggered every time someone asks a new question via the question feature.

```javascript
questionNew\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    questionText: "Do you know why TikTok has such a complicated API?",
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
    rollowRole: 0, // 0 = none; 1 = follower; 2 = friends
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...jpeg"
        ]
    },
    followInfo: {
        followingCount: 982,
        followerCount: 175,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null
}
```
</p></details>
<br>

### `linkMicBattle`
Triggered every time a battle starts.

```javascript
linkMicBattle\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    battleUsers: [
        {
            userId: "6901252963970515973", // Host
            uniqueId: "growsa_fluffynation",
            nickname: "GrowSA_FluffyNation",
            profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            userBadges: [],
            userDetails: {
                profilePictureUrls: [
                    "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
                    "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...jpeg"
                ]
            },
            isModerator: false,
            isNewGifter: false,
            isSubscriber: false,
            topGifterRank: null
        },
        {
            userId: "262781145296064512", // Guest
            uniqueId: "real_martinpinkysmith",
            nickname: "Martin Pinky Smith",
            profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
            userBadges: [],
            userDetails: {
                profilePictureUrls: [
                    "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
                    "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...jpeg"
                ]
            },
            isModerator: false,
            isNewGifter: false,
            isSubscriber: false,
            topGifterRank: null
        }
    ]
}
```
</p></details>
<br>

### `linkMicArmies`
Triggered every time a battle participant receives points. Contains the current status of the battle and the army that suported the group.

```javascript
linkMicArmies\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    battleStatus: 1,
    battleArmies: [
        {
            hostUserId: "6842213780475085829",
            points: 0,
            participants: []
        },
        {
            hostUserId: "6722878711857579013",
            points: 33,
            participants: [
                {
                    userId: "7122168301669204994",
                    secUid: "",
                    nickname: "🦋",
                    profilePictureUrl: null,
                    userBadges: [],
                    userDetails: {
                        createTime: "0",
                        bioDescription: ""
                    },
                    isModerator: false,
                    isNewGifter: false,
                    isSubscriber: false,
                    topGifterRank: null
                },
                {
                    userId: "7112729060212966406",
                    secUid: "",
                    nickname: "ealkaabi44",
                    profilePictureUrl: null,
                    userBadges: [],
                    userDetails: {
                        createTime: "0",
                        bioDescription: ""
                    },
                    isModerator: false,
                    isNewGifter: false,
                    isSubscriber: false,
                    topGifterRank: null
                },
                {
                    userId: "7006435669158708229",
                    secUid: "",
                    nickname: "worood🦁 🌹🌹🌹🌹",
                    profilePictureUrl: null,
                    userBadges: [],
                    userDetails: {
                        createTime: "0",
                        bioDescription: ""
                    },
                    isModerator: false,
                    isNewGifter: false,
                    isSubscriber: false,
                    topGifterRank: null
                }
            ]
        }
    ]
}
```
</p></details>
<br>

### `liveIntro`
Triggered when a live intro message appears.

```javascript
liveIntro\0{data}
```
<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    id: "1658723381",
    description: "welcome to my broadcast!",
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
    followRole: 0,
    userBadges: [
        {
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p77-sign-va.tiktokcdn.com/tos-maliva-avt-0...webp",
            "https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0...jpeg"
        ]
    },
    followInfo: {
        followingCount: 886,
        followerCount: 57141,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null
}
```
</p></details>

<br>

### `subscribe`
Triggers when a user creates a subscription.

```javascript
subscribe\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    subMonth: 1,
    oldSubscribeStatus: 2,
    subscribingStatus: 1,
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
    followRole: 0,
    userBadges: [],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...webp",
            "https://p16-sign-sg.tiktokcdn.com/aweme/100x100/to...jpeg"
        ]
    },
    followInfo: {
        followingCount: 23,
        followerCount: 43,
        followStatus: 0,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137745705032043266",
    createTime: "1661885986187",
    displayType: "pm_mt_subinfo_user",
    label: "{0:user} just subscribed to the host"
}
```
</p></details>

<br>

### Custom Events
These events are based on message events.
<br>

### `follow`
Triggers when a user follows the streamer. Based on `social` event.

```javascript
follow\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
    followRole: 1,
    userBadges: [
        {
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p19-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...jpeg"
        ]
    },
    followInfo: {
        followingCount: 277,
        followerCount: 96,
        followStatus: 1,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750889884076842",
    createTime: "1661887134629",
    displayType: "pm_main_follow_message_viewer_2",
    label: "{0:user} followed the host"
}
```
</p></details>

<br>

### `share`
Triggers when a user shares the stream. Based on `social` event.

```javascript
share\0{data}
```

<details><summary>⚡ Show Data Structure</summary><p>

```javascript
{
    userId: "6813181309701719620",
    secUid: "<redacted>",
    uniqueId: "zerodytester",
    nickname: "Zerody Tester",
    profilePictureUrl: "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
    followRole: 1,
    userBadges: [
        {
            type: "pm_mt_moderator_im",
            name: "Moderator"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/rankl...image"
        },
        {
            type: "image",
            displayType: 1,
            url: "https://p19-webcast.tiktokcdn.com/webcast-va/....~...image"
        }
    ],
    userDetails: {
        createTime: "0",
        bioDescription: "",
        profilePictureUrls: [
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p19-sign.tiktokcdn-us.com/tos-useast5-avt-...webp",
            "https://p16-sign.tiktokcdn-us.com/tos-useast5-avt-...jpeg"
        ]
    },
    followInfo: {
        followingCount: 277,
        followerCount: 96,
        followStatus: 1,
        pushStatus: 0
    },
    isModerator: false,
    isNewGifter: false,
    isSubscriber: false,
    topGifterRank: null,
    msgId: "7137750889884076842",
    createTime: "1661887134629",
    displayType: "pm_mt_guidance_share",
    label: "{0:user} shared the live"
}
```
</p></details>

<br>
