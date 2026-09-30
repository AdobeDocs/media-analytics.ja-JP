---
title: 状態終了
description: メディアプレーヤーが追跡されたプレーヤー状態から離脱したことを示す信号。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%
---

# 状態終了

ステートエンドイベントは、メディアプレーヤーがフルスクリーン、ミュート、クローズドキャプションなどのトラッキングされた状態から離脱したことを示します。 [状態の開始](state-start.md)によって開かれた状態を閉じるように送信します。 状態は、同じイベントコールで開始および終了できます。 プレイヤーは複数のステートを同時に終了できます。

有効な状態名：`fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)、[状態開始](state-start.md)
* **関連する指標**：状態によって異なります。[&#x200B; プレーヤーの状態を追跡](/help/implementation/events/player-state/overview.md)を参照してください

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

適切な`MediaConstants.PlayerState`定数から作成された状態オブジェクトで`trackPlayerStateEnd`を使用します。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

適切な`MediaConstants.PlayerState`定数から作成された状態オブジェクトで`trackPlayerStateEnd`を使用します。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

適切な`ADB.Media.PlayerState`定数で`ADB.Media.createStateObject`を使用します。

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

適切な`ADBMobile.media.PlayerState`定数で`ADBMobile.media.createStateObject`を使用します。

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Roku 2.x SDKでは、プレイヤーの状況トラッキングは利用できません。 プレイヤーの状態をトラッキングするには、[Roku Edge SDK](/help/implementation/edge/roku.md)を使用します。

>[!TAB Media Collection API]

`stateEnd`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)に送信します：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
