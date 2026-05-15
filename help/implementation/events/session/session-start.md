---
title: セッション開始
description: メディアセッションの開始を通知し、後続のすべてのイベントに必要なセッション IDを取得します。
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# セッション開始

セッション開始イベントは、メディアトラッキングセッションを開きます。 再生のために最初に送信されるイベントである必要があります。 応答は、同じセッションの後続のすべてのイベントに含める必要があるセッション IDを返します。

セッションは、**10分間イベントを受信しなかった場合、**&#x200B;または&#x200B;**30分間の再生ヘッドの移動がない場合、**&#x200B;に自動的に期限切れになります。 セッションの有効期限が切れた場合は、新しいセッション IDを取得するために、「セッション開始」を再度呼び出す必要があります。

* **前提条件**：なし。常に最初のイベント
* **関連する指標**: [ メディア開始](/help/reporting/metrics/media-starts.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)に`eventType: "media.sessionStart"`と必須`sessionDetails`を呼び出します。 応答には、`handle[].payload[].sessionId` （タイプ `media-analytics:new-session`）のセッション IDが含まれています。 この値を保存し、後続のすべてのイベントで`sessionID`として渡します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

メディアオブジェクトとオプションのメタデータを使用して`trackSessionStart`を呼び出します。

**iOS （Swift）**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku （BrightScript）

必要なセッションの詳細を含めて`createMediaSession`を呼び出します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します。 応答には、`handle[].payload[].sessionId` （タイプ `media-analytics:new-session`）のセッション IDが含まれています。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## メディア SDK

`ADB.Media.createMediaObject`を使用して作成されたメディアオブジェクトで`trackSessionStart`を呼び出します：

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## メディアコレクション API

`sessionStart`件の投稿を[ セッションエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)に送信します。 応答`Location` ヘッダーには、後続のすべてのイベント要求で使用するセッション IDが含まれています。

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
