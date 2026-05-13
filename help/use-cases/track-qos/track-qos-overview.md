---
title: エクスペリエンス品質のトラッキング
description: メディア SDK を使用した Quality of Experience（QoE、QoS）追跡の概要です。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 99%

---

# 概要{#overview}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

Quality of Experience の追跡には、サービス品質（QoS）およびエラー追跡が含まれますが、どちらもオプションの要素で、コアメディアトラッキングの実装には&#x200B;**不要**&#x200B;です。 メディアプレーヤー API を使用して、QoS とエラーの追跡に関連する変数を識別できます。 Quality of Experience を追跡するうえで重要な要素は次のとおりです。

## プレーヤーイベント {#player-events}

### QoS 指標の変更時：

再生の QoS オブジェクトインスタンスを作成または更新します。 [QoS API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### すべてのビットレート変更イベント時

を呼び出します `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## QOSの実装

1. メディアの再生中にいつ QoS 指標が変更されるかを識別し、QoS 情報を使用して `MediaObject` を作成し、新しい QoS 情報を更新します。

   QoSObject 変数：

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

   | 変数 | 説明 | 必須 |
   | --- | --- | :---: |
   | `bitrate` | 現在のビットレート | ○ |
   | `startupTime` | 起動時間 | ○ |
   | `fps` | FPS の値 | ○ |
   | `droppedFrames` | ドロップフレームの数 | ○ |

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します。

   >[!IMPORTANT]
   >
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。 これにより、最も正確な QoS データを取得できます。

以下のサンプルコードでは、HTML5 メディアプレーヤー用の JavaScript 2.x SDK を使用しています。 このコードをコアメディア再生コードと共に使用する必要があります。

```js
var mediaDelegate = new MediaHeartbeatDelegate();
...  

// This is called periodically by MediaHeartbeat instance
mediaDelegate.prototype.getQoSObject = function() {
    return this.qosInfo;
};

if (e.type == "qos_update") {
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>);
    mediaDelegate.qosInfo = qosInfo;
};

if (e.type == "bitrate_change") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
};
```
