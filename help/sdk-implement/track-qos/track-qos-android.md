---
seo-title: Android での Quality of Experience の追跡
title: Android での Quality of Experience の追跡
uuid: 81ff3939-48a6-45c1-8837- ddfa33490559
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android での Quality of Experience の追跡{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 実装QoS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject 変数：

   >[!TIP]
   >
   >これらの変数は、QoSを追跡する場合にのみ必要です。

   | 変数 | 説明 | 必須 |
   | --- | --- | :---: |
   | `bitrate` | 現在のビットレート | ○ |
   | `startupTime` | 起動時間 | ○ |
   | `fps` | FPS の値 | ○ |
   | `droppedFrames` | ドロップフレームの数 | ○ |

   QoS オブジェクトの作成：

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します。

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >QoSオブジェクトを更新し、ビットレート変更ごとにビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。

