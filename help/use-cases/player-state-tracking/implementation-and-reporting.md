---
title: 実装とレポート
description: プレーヤーステートのトラッキング機能を実装する方法について説明します。
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# 実装とレポート

再生セッション中は、各ステートの発生（最初から最後まで）を個別に追跡する必要があります。 Media SDKとMedia Collection APIは、この機能のトラッキングメソッドを提供します。

Media SDKには、カスタムステートトラッキング用に2つのメソッドが含まれています。

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection APIには、必須パラメーターとして`media.stateName`を持つ2つのイベントが含まれています。

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

個々のステートに対して提供される指標は、データパラメーターとして計算して Adobe Analytics にプッシュされ、レポート目的で保存されます。 各ステートに対して 3 つの指標を使用できます。

* `a.media.states.[state.name].set = true`：ストリームの特定の再生 1 回あたり、ステートが 1 回以上設定された場合は、true に設定します。
* `a.media.states.[state.name].count = 4`：ストリームを 1 回再生する間に、ステートが発生した回数を識別します。
* `a.media.states.[state.name].time = 240`：ストリームの再生 1 回あたりの、ステートの合計時間を秒単位で識別します。

## レポート

レポートスイートでプレーヤーステートトラッキングが有効にされると、すべてのプレーヤーステート指標を、Analysis Workspace で使用可能な任意のレポートビジュアライゼーションやコンポーネント（セグメント、計算指標）に使用できます。 これらの指標は、Media Reporting Setup （設定を編集/Media Management/Media Reporting）を使用して、個々のレポートに対してAdmin Consoleから有効にできます。

![](assets/report-setup.png)

Analysis Workspaceでは、すべての新しいプロパティが指標パネルにあります。 例えば、`full screen` で検索し、指標パネルにフルスクリーンデータを表示できます。

![](assets/full-screen-report.png)

## Adobe Experience Platform にプレーヤーステート指標を読み込む

Analytics に保存されたデータはどのような目的でも使用でき、プレーヤーステート指標は XDM を使用して Adobe Experience Platform に読み込み、Customer Journey Analytics で使用することができます。 標準ステートのプロパティには固有のプロパティがあります。カスタムステートのプロパティは、カスタムイベントを介して使用できます。
