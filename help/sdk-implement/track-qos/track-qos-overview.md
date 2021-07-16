---
title: エクスペリエンス品質のトラッキング
description: メディア SDK を使用した Quality of Experience（QoE、QoS）追跡の概要です。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 100%

---

# 概要{#overview}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

Quality of Experience の追跡には、サービス品質（QoS）およびエラー追跡が含まれますが、どちらもオプションの要素で、コアメディアトラッキングの実装には&#x200B;**不要**&#x200B;です。メディアプレーヤー API を使用して、QoS とエラーの追跡に関連する変数を識別できます。Quality of Experience を追跡するうえで重要な要素は次のとおりです。

## プレーヤーイベント {#player-events}

### QoS 指標の変更時：

再生の QoS オブジェクトインスタンスを作成または更新します。[QoS API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### すべてのビットレート変更イベント時

を呼び出します `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## QoS の実装

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
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。

以下のサンプルコードでは、HTML5 メディアプレーヤー用の JavaScript 2.x SDK を使用しています。このコードをコアメディア再生コードと共に使用する必要があります。

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
