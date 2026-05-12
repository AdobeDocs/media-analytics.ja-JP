---
title: インフォーカス
description: プレーヤーがビューアの画面にいつフォーカスしているかを追跡し、バックエンドでフォーカスエンゲージメントをレポートできます。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 9%

---


# インフォーカス

>[!BEGINSHADEBOX]

*このページでは、**In focus**&#x200B;プレーヤー状態のデータ収集について説明します。 対応するレポート指標については、[&#x200B; フォーカスの影響を受けるストリーム &#x200B;](/help/reporting/metrics/in-focus-streams-impacted.md)、[&#x200B; フォーカスのカウント &#x200B;](/help/reporting/metrics/in-focus-count.md)および[&#x200B; フォーカスの合計期間](/help/reporting/metrics/in-focus-total-duration.md)を参照してください。*

>[!ENDSHADEBOX]

フォーカスプレーヤーの状態は、プレーヤーが視聴者の注意を引いたときに追跡されます。 プレーヤーがフォーカスを得たときに状態スタートイベント（通常はプレーヤーのタブまたはウィンドウがアクティブになったとき）を起動し、プレーヤーがフォーカスを失ったときに状態エンドイベントを起動します。 バックエンドでは、これらのイベントから、影響を受けるストリーム、状態エントリの数、状態の合計時間という3つの指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **XDM コレクションフィールド** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)および[`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （`name: "inFocus"`を含むエントリ） |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 状態開始、状態終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

プレイヤーがフォーカスを失った場合、`statesEnd`の状態で別のイベントを送信します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## モバイル SDK

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.IN_FOCUS`定数と共に使用します。

**iOS （Swift）**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android （Kotlin）**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

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
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

プレイヤーがフォーカスを失った場合、`statesEnd`の状態で別のイベントを送信します。

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の`inFocus`で呼び出します（プレーヤーがフォーカスを失った場合は`statesEnd`）。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.createStateObject`と`ADB.Media.PlayerState.InFocus`定数を使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## メディアコレクション API

プレイヤーがフォーカスを得たときに`stateStart` POST リクエストを送信し、フォーカスが失われたときに`stateEnd` POSTを送信します。

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
