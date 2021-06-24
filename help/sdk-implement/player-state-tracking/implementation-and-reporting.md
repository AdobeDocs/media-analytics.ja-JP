---
title: 実装とレポート
description: を含む、プレーヤーステートトラッキング機能の実装方法について説明します。
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 96%

---

# 実装とレポート

再生セッション中は、各ステートの発生（最初から最後まで）を個別に追跡する必要があります。メディア SDK とメディアコレクション API は、この機能の新しいトラッキングメソッドを提供します。

メディア SDK には、カスタムステートトラッキングの 2 つの新しいメソッドが含まれています。

`trackStateStart("state_name")`

`trackStateClose("state_name")`


メディアコレクション API には、必須イベントパラメーターが「`media.stateName`」の 2 つの新しいイベントが含まれています。

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

レポートスイートでプレーヤーステートトラッキングが有効にされると、すべてのプレーヤーステート指標を、Analysis Workspace で使用可能な任意のレポートビジュアライゼーションやコンポーネント（セグメント、計算指標）に使用できます。新しい指標は、Admin Console のメディアレポート設定（設定の編集／メディア管理／メディアレポート）で、個々のレポートに対して有効にできます。

![](assets/report-setup.png)

Analytics Workspace では、すべての新しいプロパティが指標パネルに表示されます。例えば、`full screen` で検索し、指標パネルにフルスクリーンデータを表示できます。

![](assets/full-screen-report.png)

## Adobe Experience Platform にプレーヤーステート指標を読み込む

Analytics に保存されたデータはどのような目的でも使用でき、プレーヤーステート指標は XDM を使用して Adobe Experience Platform に読み込み、Customer Journey Analytics で使用することができます。標準ステートのプロパティには固有のプロパティがあります。カスタムステートのプロパティは、カスタムイベントを介して使用できます。標準のステートプロパティについて詳しくは、[プレーヤーステートパラメーター](/help/metrics-and-metadata/player-state-parameters.md) ページで、*XDM ID のプロパティリスト*&#x200B;の節を参照してください。
