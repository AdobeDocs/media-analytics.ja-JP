---
title: JavaScript での Quality of Experience の追跡
description: このトピックでは、ブラウザーアプリ(JS)でMedia SDKを使用したエクスペリエンスの質(QoE、QoS)トラッキングの実装について説明します。
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript での Quality of Experience の追跡{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QOSの実装

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

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

   QoS オブジェクトの作成：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します。

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >QoSオブジェクトを更新し、ビットレート変更が行われるたびにビットレート変更イベントを呼び出します。 これにより、最も正確な QoS データを取得できます。

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

