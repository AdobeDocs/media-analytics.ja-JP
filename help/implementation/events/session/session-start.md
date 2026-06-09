---
title: セッション開始
description: メディアセッションの開始を通知し、後続のすべてのイベントに必要なセッション IDを取得します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---


# セッション開始

セッション開始イベントは、メディアトラッキングセッションを開きます。 再生のために最初に送信されるイベントである必要があります。 応答は、同じセッションの後続のすべてのイベントに含める必要があるセッション IDを返します。

セッションは、**10分間イベントを受信しなかった場合、**&#x200B;または&#x200B;**30分間の再生ヘッドの移動がない場合、**&#x200B;に自動的に期限切れになります。 セッションの有効期限が切れた場合は、新しいセッション IDを取得するために、「セッション開始」を再度呼び出す必要があります。

* **前提条件**：なし。常に最初のイベント
* **関連する指標**: [[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md)

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

メディアオブジェクトとオプションのメタデータを使用して`trackSessionStart`を呼び出します。

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

メディアオブジェクトとオプションのメタデータを使用して`trackSessionStart`を呼び出します。

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

`ADBMobile.media.createMediaObject`を使用して作成されたメディアオブジェクトで`trackSessionStart`を呼び出します：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "video-123",                        // name
  "video-id-123",                     // media ID
  128,                                // length (seconds)
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);

ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`adb_media_init_mediainfo`でメディアオブジェクトを作成し、`mediaTrackSessionStart`を呼び出します。 オプションの2番目の引数は、`a.media.*`個のメタデータキーまたは`invalid`の連想配列を受け入れます。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`sessionStart`件の投稿を[&#x200B; セッションエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)に送信します。 応答`Location` ヘッダーには、後続のすべてのイベント要求で使用するセッション IDが含まれています。

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

>[!ENDTABS]

## セッションの再開

以前に閉じられたセッションを再開する場合（例えば、クロスデバイスのハンドオフ後、またはアプリケーションが保存された再生状態を復元した後など）、セッションの開始時に再開フラグを設定します。 これにより、Analyticsは[[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md)ではなく[[!UICONTROL &#x200B; コンテンツ再開]](/help/reporting/metrics/content-resumes.md)を増分します。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

`hasResume: true`を`sessionDetails`に追加：

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
        streamType: "video",
        hasResume: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

`trackSessionStart`を呼び出す前に、メディアオブジェクトに`resumed` キーを設定します。

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

mediaObject[MediaConstants.MediaObjectKey.resumed] = true
tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

`trackSessionStart`を呼び出す前に、メディアオブジェクトに`RESUMED` キーを設定します。

```kotlin
val mediaObject = Media.createMediaObject("video-123", "video-id-123", 128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

mediaObject[Media.MediaObjectKey.RESUMED] = true
tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Edge六]

`"hasResume": true`を`sessionDetails`に追加：

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`"hasResume": true`を`sessionDetails`に追加：

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
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

メディアオブジェクトに`MediaResumed` キーを設定します。

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video
);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;
tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

メディアオブジェクトに`MediaResumed` キーを設定します。

```javascript
var mediaObject = ADBMobile.media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video
);

mediaObject[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaObject, null);
```

>[!TAB Roku 2.x]

`mediaTrackSessionStart`を呼び出す前に、メディアオブジェクトに`resumed` キーを設定します。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)
mediaInfo.resumed = true

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`"media.resume": true`を`params` オブジェクトに追加します：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123",
    "media.resume": true
  }
}
```

>[!ENDTABS]
