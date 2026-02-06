---
title: 複数プレーヤーの状態を一度に更新する
description: このトピックでは、複数プレーヤーの状態のトラッキング機能について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---

# 複数プレーヤーの状態のトラッキング

次の図に示すように、2 つのプレーヤーの状態が同時に開始および終了したり、状態の終了が別の状態の開始になったりする場合があります。

![複数プレーヤーの状態](assets/multiple-player-states.png)

現在の実装では、次の両方のシナリオを使用できます。
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

ただし、この場合は、複数の `stateStart` および `stateEnd` イベントを発行して、複数の同時状態変化を通知する必要があります。この一般的な動作を最適化するために、`statesUpdate`
イベントタイプが実装されました。これは、状態のリストを終了し、新しい状態のリストを開始します。


新しい `statesUpdate` イベントを使用すると、上記のイベントのリストは次のようになります。
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

同じ動作に対して、状態更新呼び出しの数が 6 から 3 に減少しました。 最後のイベントは単純な `stateEnd(fullScreen)` だった可能性もあります。


## Media Collection API の実装 {#mpst-api}

Media Collection API を使用して、複数プレーヤーの状態のトラッキングを実装できます。

### 例

次に、複数プレーヤーの状態のトラッキング用の Media Collection API の実装例を示します。

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## メディア SDK の実装

メディア SDK の実装はありません。
