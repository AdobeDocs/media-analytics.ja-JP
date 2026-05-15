---
title: ミュート
description: ビューアがオーディオをミュートおよびミュート解除するタイミングを追跡して、バックエンドがミュートエンゲージメントを報告できるようにします。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 10%

---


# ミュート

>[!BEGINSHADEBOX]

*このページでは、**Mute**プレーヤー状態のデータ収集について説明します。 対応するレポート指標について、[ ミュート ](/help/reporting/metrics/mute-streams-impacted.md)、[ ミュート数](/help/reporting/metrics/mute-count.md)、および[ ミュート合計期間](/help/reporting/metrics/mute-total-duration.md)の影響を受けるストリームを参照してください。*

>[!ENDSHADEBOX]

ビューアがオーディオをミュートおよびミュート解除すると、ミュートプレーヤーの状態が追跡されます。 ビューアのミュート時に状態開始イベントを起動し、ビューアのミュート解除時に状態終了イベントを起動します。 バックエンドでは、これらのイベントから、影響を受けるストリーム、状態エントリの数、状態の合計時間という3つの指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **XDM コレクションフィールド** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)および[`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （`name: "mute"`を含むエントリ） |
| **Audience Manager特性** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [状態開始](/help/implementation/events/player-state/state-start.md)、[状態終了](/help/implementation/events/player-state/state-end.md) |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

ビューアーがミュートを解除すると、状態が`statesEnd`の別のイベントを送信します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## モバイル SDK

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.MUTE`定数と共に使用します。

**iOS （Swift）**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android （Kotlin）**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

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
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

ビューアーがミュートを解除すると、状態が`statesEnd`の別のイベントを送信します。

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の`mute`で呼び出します（ビューアがミュートを解除すると`statesEnd`になります）。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.createStateObject`と`ADB.Media.PlayerState.Mute`定数を使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## メディアコレクション API

視聴者がミュートしているときに`stateStart` POST リクエストを送信し、ミュートを解除しているときに`stateEnd` POST リクエストを送信します。

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
