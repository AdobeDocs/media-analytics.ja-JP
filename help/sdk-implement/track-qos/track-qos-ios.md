---
title: iOS での Quality of Experience の追跡
description: ここでは、iOS でのメディア SDK を使用した Quality of Experience（QoE、QoS）追跡の実装について説明します。
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS での Quality of Experience の追跡 {#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

## QoS の実装

1. メディアの再生中にいつビットレートが変更されるかを識別し、QoS 情報を使用して `MediaObject` インスタンスを作成します。

   QoSObject 変数：

   | 変数 | 説明 | 必須 |
   | --- | --- | :---: |
   | `bitrate` | 現在のビットレート | ○ |
   | `startupTime` | 起動時間 | ○ |
   | `fps` | FPS の値 | ○ |
   | `droppedFrames` | ドロップフレームの数 | ○ |

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

   QoS オブジェクトの作成：

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. `getQoSObject` メソッドで、最新の QoS 情報が返されるようにします。
1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します。

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。

