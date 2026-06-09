---
title: フルスクリーン
description: ビューアがフルスクリーン再生を開始および終了するタイミングを追跡し、バックエンドがフルスクリーンのエンゲージメントをレポートできるようにします。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---


# フルスクリーン

>[!BEGINSHADEBOX]

*このページでは、**フルスクリーン**&#x200B;プレーヤーの状態に関するデータ収集について説明します。 対応するレポート指標については、[&#x200B; フルスクリーンの影響を受けるストリーム &#x200B;](/help/reporting/metrics/full-screen-streams-impacted.md)、[&#x200B; フルスクリーン数](/help/reporting/metrics/full-screen-count.md)、および[&#x200B; フルスクリーン合計期間](/help/reporting/metrics/full-screen-total-duration.md)を参照してください。*

>[!ENDSHADEBOX]

フルスクリーンプレーヤーの状態は、ビューアがフルスクリーン再生を開始および終了したときに追跡されます。 ビューアがフルスクリーンに入るたびに、ビューアが終了したときにステートエンドイベントを起動します。 バックエンドでは、これらのイベントから、影響を受けるストリーム、状態エントリの数、状態の合計時間という3つの指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)および[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （`name: "fullscreen"`を含むエントリ） |
| **Audience Manager特性** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [状態開始](/help/implementation/events/player-state/state-start.md)、[状態終了](/help/implementation/events/player-state/state-end.md) |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

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

ビューアがフルスクリーンを終了したら、状態が`statesEnd`の別のイベントを送信します。

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

>[!TAB iOS]

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.FULLSCREEN`定数と共に使用します。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.FULLSCREEN`定数と共に使用します。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Edge六]

`sendMediaEvent`を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

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

ビューアがフルスクリーンを終了したら、状態が`statesEnd`の別のイベントを送信します。

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

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の`fullscreen`で呼び出します（ビューアが終了すると`statesEnd`になります）。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.createStateObject`と`ADB.Media.PlayerState.FullScreen`定数を使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Chromecastには`PlayerState`という名前の定数がないので、`ADBMobile.media.createStateObject`を`"fullscreen"`文字列で直接使用します。

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Roku 2.x SDKでは、プレイヤーの状況トラッキングは利用できません。 プレイヤーの状態をトラッキングするには、[Roku Edge SDK](/help/implementation/edge/roku.md)を使用します。

>[!TAB Media Collection API]

視聴者がフルスクリーンに入ったときに`stateStart` POST リクエストを送信し、視聴者が終了したときに`stateEnd` POSTを送信します。

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
