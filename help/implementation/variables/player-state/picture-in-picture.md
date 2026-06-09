---
title: ピクチャインピクチャ
description: ビューアがピクチャインピクチャ再生を開始および終了するタイミングを追跡して、バックエンドがPiP エンゲージメントをレポートできるようにします。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 5%

---


# ピクチャインピクチャ

>[!BEGINSHADEBOX]

*このページでは、**写真**&#x200B;プレーヤーの状態のデータ収集について説明します。 対応するレポート指標については、[画像の影響を受けるストリーム &#x200B;](/help/reporting/metrics/picture-in-picture-streams-impacted.md)、[画像のカウント &#x200B;](/help/reporting/metrics/picture-in-picture-count.md)、および[画像の合計期間](/help/reporting/metrics/picture-in-picture-total-duration.md)を参照してください。*

>[!ENDSHADEBOX]

ピクチャーインピクチャーの状態は、ビューアがピクチャーインピクチャー再生に出入りしたときに追跡されます。 ピクチャインピクチャが開始されたときにステートスタートイベントを起動し、終了したときにステートエンドイベントを起動します。 バックエンドでは、これらのイベントから、影響を受けるストリーム、状態エントリの数、状態の合計時間という3つの指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)および[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （`name: "pictureInPicture"`を含むエントリ） |
| **Audience Manager特性** | `c_contextdata.a.media.states.pictureinpicture.set`, `c_contextdata.a.media.states.pictureinpicture.count`, `c_contextdata.a.media.states.pictureinpicture.time` |
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
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

ビューアがピクチャーインピクチャを終了したら、別のイベントを`statesEnd`の状態で送信します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.PICTURE_IN_PICTURE`定数と共に使用します。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

`tracker.trackPlayerStateStart()`と`tracker.trackPlayerStateEnd()`を`MediaConstants.PlayerState.PICTURE_IN_PICTURE`定数と共に使用します。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Edge六]

`sendMediaEvent`を使用して、状態が`statesStart`に追加された`media.statesUpdate` イベントを送信します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

ビューアがピクチャーインピクチャを終了したら、別のイベントを`statesEnd`の状態で送信します。

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) エンドポイントを`statesStart`の`pictureInPicture`で呼び出します（ビューアがPiPを終了すると`statesEnd`になります）。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
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

`ADB.Media.createStateObject`と`ADB.Media.PlayerState.PictureInPicture`定数を使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Chromecastには`PlayerState`という名前の定数がないので、`ADBMobile.media.createStateObject`を`"pictureInPicture"`文字列で直接使用します。

```javascript
var stateObject = ADBMobile.media.createStateObject("pictureInPicture");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer exits picture-in-picture:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Roku 2.x SDKでは、プレイヤーの状況トラッキングは利用できません。 プレイヤーの状態をトラッキングするには、[Roku Edge SDK](/help/implementation/edge/roku.md)を使用します。

>[!TAB Media Collection API]

ピクチャインピクチャが開始されたときに`stateStart` POST リクエストを送信し、終了したときに`stateEnd` POSTを送信します。

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
