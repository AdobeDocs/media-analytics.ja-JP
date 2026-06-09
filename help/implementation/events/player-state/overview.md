---
title: プレイヤーの状態を追跡
description: プレーヤーの状態イベントと、フルスクリーン、ミュート、クローズドキャプション、ピクチャインピクチャ、インフォーカス状態を追跡する方法について説明します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 12%

---


# プレイヤーの状態を追跡

プレーヤーの状態イベント セッション全体を通じて、視聴者がプレーヤーのコントロールとどのようにインタラクションするかを追跡します。 これらはオプションであり、コアメディアトラッキングの実装には必要ありません。 追跡可能な5つの状態：`fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、および`inFocus`。

プレーヤーの状態イベントは、ビューアがクローズドキャプションやミュートを有効にする頻度など、アクセシビリティ機能の使用状況を把握するのに役立ちます。 また、フルスクリーンやインライン表示、ピクチャーインピクチャーのマルチタスク処理など、視聴行動パターンも明らかになります。

## プレーヤーイベント

| プレイヤーイベント | アクション |
| --- | --- |
| プレイヤーがステートに入る | コール状態の開始 |
| プレイヤーがステートを終了 | 呼び出し状態終了 |

## 標準ステートとカスタムステート

5 つの標準プレーヤーステートがあり、独自のカスタムステートを追加できます。

| 標準の状態名 | メディア SDK の定数 | メディアコレクション API の名前 |
|----|----|----|
| フルスクリーン | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| クローズドキャプション | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| ミュート | `ADB.Media.PlayerState.Mute` | `mute` |
| ピクチャインピクチャ | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| インフォーカス | `ADB.Media.PlayerState.InFocus` | `inFocus` |

XDM パスと指標の定義を含む完全な変数参照については、[Player状態変数](/help/implementation/variables/player-state/)を参照してください。

**カスタム状態：** カスタム状態を作成して、アプリケーションに固有の追加のプレーヤー行動をキャプチャできます。 カスタム状態オブジェクトの作成について詳しくは、[Media API リファレンス：`createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)を参照してください。

## 実装手順

1. **プレイヤーが追跡可能な5つの状態のいずれかを入力すると、[状態の開始](state-start.md)**&#x200B;を呼び出します。 複数のステートを同時にアクティブにすることができ、同じイベント呼び出しで複数のステートを開始できます。
1. **プレーヤーが状態を終了すると、[状態の終了](state-end.md)**&#x200B;を呼び出します。 複数のステートを同じイベント呼び出しで終了させることができ、ステートを1回の呼び出しで開始して終了させることができます。

## ガイドライン

* 1 つのビデオセッションでは、最大 10 のプレーヤーステートを使用できます。
* ステートの組み合わせは自由です。
* 複数のプレーヤー状態が渡された場合、最初の10のみが保持され、メディアバックエンドにダウンストリームで転送されます。
* 最大10個のステートは、開いているか閉じているかに関係なく、すべてのステートに適用されます。
* 状態は複数回開始および終了でき、単一の状態としてカウントされます。 例えば、`closedCaptioning`は5回開始および停止できますが、1つの状態としてカウントされます。
* プレーヤーステートは、すべての再生ステートで（分割せずに）計算されます。
* プレーヤーの状態は、個々の再生セッションごとにキャプチャされます。 プレイバック全体でプレイヤーの状態が計算されない。
* 状態が停止した後も、アプリケーションのステータスに関する情報は保持されません。 ステートの終了後にトラッキングを続行するには、ステートを再び開始する必要があります。

## 複数のステートを同時に更新する

XDM ベースのプラットフォームでは、`statesStart`と`statesEnd`の配列を使用して、複数の状態の変更を1回の`statesUpdate`呼び出しにバッチ処理できます。 モバイル SDKでは、状態の変更ごとに個別の呼び出しが必要です。

次の例では、ミュートとピクチャインピクチャを同時に開始し、フルスクリーンに切り替えます。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDKはバッチ処理をサポートしていません。状態の変更ごとに個別の呼び出しを送信します。

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDKはバッチ処理をサポートしていません。状態の変更ごとに個別の呼び出しを送信します。

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Edge六]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

複数の状態の変更には、個別の呼び出しが必要です。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

複数の状態の変更には、個別の呼び出しが必要です。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB Roku 2.x]

Roku 2.x SDKでは、プレイヤーの状況トラッキングは利用できません。 プレイヤーの状態をトラッキングするには、[Roku Edge SDK](/help/implementation/edge/roku.md)を使用します。

>[!TAB Media Collection API]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## 長い一時停止

ビデオセッションの中断時間が30分を超える場合、APIには新しいセッションが必要です。 新しいセッション IDを生成し、すべてのアクティブな状態を保持して、新しい`sessionStart`呼び出しの直後に`stateStart` イベントで復元できるようにします。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

`sessionEnd`が送信されたら、新しいセッションを開始し、アクティブな状態をすぐに再送信します。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## 状態指標

追跡済みステートごとに3つの指標が計算され、Media Close呼び出しでAdobe Analyticsに送信されます。

| 指標 | コンテキストデータキー | 説明 |
| --- | --- | --- |
| 状態セット | `a.media.states.[state.name].set = true` | 再生中に少なくとも1回は状態が設定されている場合`true` |
| 状態数 | `a.media.states.[state.name].count = 4` | 再生中に状態が発生した回数 |
| 状態時間 | `a.media.states.[state.name].time = 240` | 再生中にステートに費やされた合計時間（秒） |
