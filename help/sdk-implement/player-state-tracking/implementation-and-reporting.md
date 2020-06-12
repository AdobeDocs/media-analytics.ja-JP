---
title: 実装とレポート
description: このトピックでは、以下を含むプレーヤーステートトラッキング機能の実装方法について説明します。
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 58%

---


# 実装とレポート

再生セッション中は、各ステートの発生（最初から最後まで）を個別に追跡する必要があります。メディア SDK とメディアコレクション API は、この機能の新しいトラッキングメソッドを提供します。

メディア SDK には、カスタムステートトラッキングの 2 つの新しいメソッドが含まれています。

`trackStateStart("state_name")`

`trackStateClose("state_name")`


The Media Collection API includes two new events that have `media.stateName` as the required parameter:

`stateStart` と `stateEnd`

## メディア SDK の実装

プレーヤーステートトラッキング

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

プレーヤーステートの終了

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## メディアコレクション API の実装

プレーヤーステートトラッキング

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

プレーヤーステートの終了

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## ステートの指標

個々のステートに対して提供される指標は、データパラメーターとして計算して Adobe Analytics にプッシュされ、レポート目的で保存されます。各ステートに対して 3 つの指標を使用できます。

* `a.media.states.[state.name].set = true`：ストリームの特定の再生 1 回あたり、ステートが 1 回以上設定された場合は、true に設定します。
* `a.media.states.[state.name].count = 4`：ストリームを 1 回再生する間に、ステートが発生した回数を識別します。
* `a.media.states.[state.name].time = 240`：ストリームの再生 1 回あたりの、ステートの合計時間を秒単位で識別します。

## レポート

レポートスイートでプレイヤー状態の追跡が有効になると、すべてのプレイヤー状態指標を、Analysis Workspaceで使用可能な任意のレポートビジュアライゼーションやコンポーネント（セグメント、計算指標）に使用できます。 新しい指標は、管理コンソールから、メディアレポート設定(設定の編集/メディア管理/メディアレポート)を使用して、個々のレポートに対して有効にできます。

![](assets/report-setup.png)

Analytics Workspaceでは、すべての新しいプロパティが指標パネルに表示されます。 例えば、指標パネルでフルスクリーンデータ `full screen` を表示で検索できます。

![](assets/full-screen-report.png)

## Adobe Experience Platform にプレーヤーステート指標を読み込む

Analytics に保存されたデータはどのような目的でも使用でき、プレーヤーステート指標は XDM を使用して Adobe Experience Platform に読み込み、Customer Journey Analytics で使用することができます。標準状態プロパティには固有のプロパティがあり、カスタム状態はカスタムイベントを使用してプロパティを使用できます。 標準の状態プロパティについて詳しくは、 *Player状態パラメーター* ページの「XDM Identitys [の](/help/metrics-and-metadata/player-state-parameters.md) プロパティリストー」の節を参照してください。
