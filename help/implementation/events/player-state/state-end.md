---
title: 状態終了
description: メディアプレーヤーが追跡されたプレーヤー状態から離脱したことを示す信号。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 13%

---


# 状態終了

ステートエンドイベントは、メディアプレーヤーがフルスクリーン、ミュート、クローズドキャプションなどのトラッキングされた状態から離脱したことを示します。 [状態の開始](state-start.md)によって開かれた状態を閉じるように送信します。 状態は、同じイベントコールで開始および終了できます。 プレイヤーは複数のステートを同時に終了できます。

有効な状態名：`fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **前提条件**: [ セッション開始](../session/session-start.md)、[状態開始](state-start.md)
* **関連する指標**：状態によって異なります。[ プレーヤーの状態トラッキング ](/help/use-cases/player-state-tracking/implementation-and-reporting.md)を参照してください

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.statesUpdate"`で呼び出し、状態名を`statesEnd`で呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

状態は、同じ呼び出しで開始および終了できます。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

適切な`MediaConstants.PlayerState`定数から作成された状態オブジェクトで`trackPlayerStateEnd`を使用します。

**iOS （Swift）**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.statesUpdate"`で呼び出し、状態名を`statesEnd`で呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesEnd`の状態名で呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

適切な`ADB.Media.PlayerState`定数で`ADB.Media.createStateObject`を使用します。

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## メディアコレクション API

`stateEnd`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
