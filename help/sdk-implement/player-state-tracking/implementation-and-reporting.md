---
title: 導入とレポート
description: このトピックでは、を含むプレイヤー状態トラッキング機能の実装方法について説明します。
translation-type: tm+mt
source-git-commit: 614780a121eac6d5f822d439365fa59f85959ce2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 導入とレポート

再生セッション中は、各状態のオカレンス(開始間)を個別に追跡する必要があります。 メディアSDKとメディアコレクションAPIは、この機能の新しいトラッキングメソッドを提供します。

メディアSDKには、カスタム状態追跡の2つの新しいメソッドが含まれています。

`trackStateStart("state_name")`

`trackStateClose("state_name")`


メディアコレクションAPIには、次の2つの新しいイベントが追加されました。これら `media.stateName` のパラメーターは、必須パラメーターとして指定します。

`stateStart` と `stateEnd`

## メディアSDKの実装

プレイヤーの状態開始

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

プレイヤー状態の終了

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## メディア収集APIの実装

プレイヤーの状態開始

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

プレイヤー状態の終了

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

## 状態指標

個々の状態に対して提供される指標は、計算され、Context DataパラメーターとしてAdobe Analyticsにプッシュされ、レポートのために保存されます。 状態ごとに3つの指標を使用できます。

* `a.media.states.[state.name].set = true`  — ストリームの特定の再生ごとに少なくとも1回状態が設定された場合、trueに設定します。
* `a.media.states.[state.name].count = 4`  — ストリームの個々の再生中に、ある状態が発生した回数を識別します。
* `a.media.states.[state.name].time = 240`  — ストリームの個々の再生あたりの状態の合計時間を秒単位で識別します。

## レポート

レポートスイートでプレイヤー状態の追跡が有効になると、すべてのプレイヤー状態指標を、分析ワークスペースやコンポーネント（セグメント、計算指標）で使用できるレポートのビジュアライゼーションに使用できます。 新しい指標は、管理コンソールから、メディアレポート設定(設定の編集/メディア管理/メディアレポート)を使用して、個々のレポートに対して有効にできます。

![](assets/report-setup.png)

Analytics Workspaceでは、すべての新しいプロパティが指標パネルに表示されます。 例えば、指標パネルでフルスクリーンデータ `full screen` を表示で検索できます。

![](assets/full-screen-report.png)

## Adobe Experience Platformへのプレイヤーの指標のインポート

Analyticsに保存されたデータはどのような目的でも使用でき、プレーヤー状態指標はXDMを使用してAdobe Experience Platformにインポートし、Customer Jeurney Analyticsで使用できます。 標準の状態プロパティには固有のプロパティがあり、カスタム状態のプロパティはカスタムイベントを介して使用できます。 詳しくは、?LINK TO METRICリスト？のXDM IDのプロパティリストを参照してください。
