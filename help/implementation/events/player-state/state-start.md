---
title: 状態の開始
description: メディアプレーヤーがトラッキング済みプレーヤー状態になったことを示す信号。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 13%

---


# 状態の開始

状態開始イベントは、メディアプレーヤーがフルスクリーン、ミュート、クローズドキャプションなどのトラッキングされた状態に入ったことを示します。 プレーヤーは複数のステートを同時に使用でき、ステートは同じイベントコールで開始および終了できます。 [状態の終了](state-end.md) イベントを含む各状態を閉じます。

有効な状態名：`fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**：状態によって異なります。[&#x200B; プレーヤーの状態トラッキング &#x200B;](/help/use-cases/player-state-tracking/implementation-and-reporting.md)を参照してください

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.statesUpdate"`で呼び出し、状態名を`statesStart`で呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

同じ呼び出しで複数のステートを開始できます。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

適切な`MediaConstants.PlayerState`定数から作成された状態オブジェクトで`trackPlayerStateStart`を使用します。

**iOS （Swift）**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.statesUpdate"`で呼び出し、状態名を`statesStart`で呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

## Media Edge API

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の状態名で呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateStart(stateObject);
```

## メディアコレクション API

`stateStart`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
