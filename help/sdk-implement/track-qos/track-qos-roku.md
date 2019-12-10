---
title: Roku での Quality of Experience の追跡
description: ここでは、Roku でのメディア SDK を使用した Quality of Experience（QoE、QoS）追跡の実装について説明します。
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku での Quality of Experience の追跡 {#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

## QoS の実装

1. メディアの再生中にいつビットレートが変更されるかを識別し、`mediaUpdateQoS` API を使用してメディア SDK の QoS 情報を更新します。

   QoSObject 変数：

   >[!TIP]
   >
   >これらの変数は、QoS を追跡している場合にのみ必要です。

   | 変数 | 説明 | 必須 |
   | --- | --- | :---: |
   | `bitrate` | 現在のビットレート | ○ |
   | `startupTime` | 起動時間 | ○ |
   | `fps` | FPS の値 | ○ |
   | `droppedFrames` | ドロップフレームの数 | ○ |

   例：

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. 再生中にビットレートが切り替わったときに、`trackEvent(BitrateChange)` を呼び出して、ビットレートが変更されたことをメディア SDK に通知します。

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >更新されたビットレート値と共に `updateQoSObject` を呼び出す必要があります。

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します（[の概要](/help/sdk-implement/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。

