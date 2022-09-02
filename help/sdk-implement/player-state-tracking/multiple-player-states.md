---
title: 複数のプレーヤーステートを一度に更新する
description: このトピックでは、複数のプレーヤーステートトラッキング機能について説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 9%

---

# 複数のプレーヤーステートトラッキング

次の図に示すように、2 つのプレーヤーステートが同時に開始および終了したり、ステートの終了が別のステートの開始になったりする場合があります。

![複数のプレーヤーステート](assets/multiple-player-states.svg)

現在の実装では、次の両方のシナリオを使用できます。
- `stateStart(pictureInPicture)` -t0
- `stateStart(mute)` -t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

ただし、この場合は、複数の `stateStart` および `stateEnd` イベントを使用して、複数の状態の同時変更を伝えることができます。 この一般的な動作を最適化するために、 `statesUpdate` イベントタイプが実装され、状態のリストを終了し、新しい状態のリストを開始します。

新しい `statesUpdate` イベントの場合、上記のイベントのリストは次のようになります。
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` -t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

同じ動作に対して、状態更新呼び出しの数が 6 から 3 に減少しました。 最後のイベントも単純なものでした `stateEnd(fullScreen)`.

## メディアコレクション API の実装 {#mpst-api}

メディアコレクション API を使用して、複数のプレーヤーステートトラッキングを実装できます。

### 例

次に、複数のプレーヤーステートトラッキングのためのメディアコレクション API の実装例を示します。

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
