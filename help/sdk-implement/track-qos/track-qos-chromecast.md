---
seo-title: Chromecast での Quality of Experience の追跡
title: Chromecast での Quality of Experience の追跡
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Chromecast での Quality of Experience の追跡{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 概要 {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. メディアプレイヤーAPIを使用して、QoSおよびエラー追跡に関連する変数を識別できます。

## Player events {#player-events}

### すべてのビットレート変更イベント

* 再生の QoS オブジェクトインスタンス（`qosObject`）を作成または更新します
* 呼び出し `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### プレーヤーのエラー時

呼び出し `trackError(“media error id”);`

## 実装方法 {#section_3B8EBEB167624D0481E8AF4761F83047}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **QoSObject 変数：**

   >[!TIP]
   >
   >これらの変数は、QoSを追跡する場合にのみ必要です。

   | 変数 | 説明 | 必須 |
   | --- | --- | :---: |
   | `bitrate` | 現在のビットレート | ○ |
   | `startupTime` | 起動時間 | ○ |
   | `fps` | FPS の値 | ○ |
   | `droppedFrames` | ドロップフレームの数 | ○ |

   **QoS オブジェクトの作成：**[createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >QoSオブジェクトを更新し、ビットレート変更ごとにビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

