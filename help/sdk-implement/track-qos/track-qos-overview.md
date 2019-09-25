---
seo-title: 概要
title: 概要
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 概要{#overview}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. メディアプレイヤーAPIを使用して、QoSおよびエラートラッキングに関連する変数を識別できます。 Quality of Experience を追跡するうえで重要な要素は次のとおりです。

## プレーヤーイベント {#player-events}

### QoS 指標の変更時：

再生の QoS オブジェクトインスタンスを作成または更新します。[QoS APIリファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### すべてのビットレート変更イベント

呼び出し `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## QOSの実装

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   QoSObject 変数：

   >[!TIP]
   >
   >これらの変数は、QoSを追跡する予定の場合にのみ必要です。

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
   >QoSオブジェクトを更新し、ビットレート変更が行われるたびにビットレート変更イベントを呼び出します。 これにより、最も正確な QoS データを取得できます。

以下のサンプルコードは、HTML5メディアプレイヤー用のJavaScript 2.x SDKを使用しています。 このコードは、コアメディア再生コードと共に使用する必要があります。

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

