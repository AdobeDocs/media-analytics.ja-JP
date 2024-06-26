---
title: Android でエクスペリエンス品質をトラッキングする方法
description: Android で Media SDK を使用してエクスペリエンス品質（QoE、QoS）のトラッキングを実装する方法を説明します。
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 98%

---

# Android でのエクスペリエンス品質の追跡{#track-quality-of-experience-on-android}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## QoS の実装

1. メディアの再生中にいつビットレートが変更されるかを識別し、QoS 情報を使用して `MediaObject` インスタンスを作成します。

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
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。
