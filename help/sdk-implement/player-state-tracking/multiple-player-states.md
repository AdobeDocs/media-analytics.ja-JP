---
title: 複数のプレーヤーステートを一度に更新する
description: このトピックでは、複数のプレーヤーステートトラッキング機能について説明します。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 10%

---

# 複数のプレーヤーステートトラッキング

2 つのプレーヤーステートが同時に開始および終了する場合や、ステートの終わりが別のステートの開始でもある場合があります。 次の例を見てみましょう。

![複数のプレーヤーステート](assets/multiple-player-states.svg)

現在の実装では、次の両方のシナリオを使用できます。
- `stateStart(pictureInPicture)` -t0
- `stateStart(mute)` -t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

ただし、クライアントは多数の `stateStart` および `stateEnd` イベントを使用して、複数の状態の同時変更を伝えることができます。 この一般的な動作を最適化するために、 `statesUpdate` イベントタイプが実装され、状態のリストを終了し、新しい状態のリストを開始します。

新しい `statesUpdate` イベントの場合、上記のイベントのリストは次のようになります。
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` -t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

同じ動作に対して、状態更新呼び出しの数が 6 から 3 に減少しました。 最後のイベントも単純なものでした `stateEnd(fullScreen)`.

## メディアコレクション API の実装

例：

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
