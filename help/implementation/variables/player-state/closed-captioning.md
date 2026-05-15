---
title: クローズドキャプション
description: ビューアがクローズドキャプションのオンとオフを切り替えたタイミングを追跡し、バックエンドがキャプションのエンゲージメントをレポートできるようにします。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 9%

---


# クローズドキャプション

>[!BEGINSHADEBOX]

*このページでは、**クローズドキャプション**プレーヤー状態のデータ収集について説明します。 対応するレポート指標について、[ クローズドキャプションの影響を受けるストリーム ](/help/reporting/metrics/closed-captioning-streams-impacted.md)、[ クローズドキャプション数](/help/reporting/metrics/closed-captioning-count.md)、および[ クローズドキャプション合計期間](/help/reporting/metrics/closed-captioning-total-duration.md)を参照してください。*

>[!ENDSHADEBOX]

クローズドキャプションプレーヤーの状態は、ビューアがキャプションのオンとオフを切り替えると追跡されます。 キャプションが有効になっている場合は状態開始イベントを起動し、キャプションが無効になっている場合は状態終了イベントを起動します。 バックエンドでは、これらのイベントから、影響を受けるストリーム、状態エントリの数、状態の合計時間という3つの指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **XDM コレクションフィールド** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)および[`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （`name: "closedCaptioning"`を含むエントリ） |
| **Audience Manager特性** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [状態開始](/help/implementation/events/player-state/state-start.md)、[状態終了](/help/implementation/events/player-state/state-end.md) |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

ビューアがキャプションを無効にした場合、`statesEnd`の状態で別のイベントを送信します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## モバイル SDK

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.CLOSED_CAPTION`定数と共に使用します。

**iOS （Swift）**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android （Kotlin）**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku （BrightScript）

`sendMediaEvent`を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

ビューアがキャプションを無効にした場合、`statesEnd`の状態で別のイベントを送信します。

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の`closedCaptioning`で呼び出します（ビューアがキャプションを無効にした場合は`statesEnd`）。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.createStateObject`と`ADB.Media.PlayerState.ClosedCaptioning`定数を使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## メディアコレクション API

キャプションが有効になっている場合は`stateStart` POST リクエストを送信し、無効になっている場合は`stateEnd` POST リクエストを送信します。

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
