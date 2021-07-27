---
title: Chromecast でエクスペリエンス品質をトラッキングする方法
description: Chromecast で Media SDK を使用してエクスペリエンス品質（QoE、QoS）のトラッキングを実装する方法について説明します。
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# Chromecast での Quality of Experience の追跡{#track-quality-of-experience-on-chromecast}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

## 概要  {#overview}

Quality of Experience の追跡には、サービス品質（QoS）およびエラー追跡が含まれますが、どちらもオプションの要素で、コアメディアトラッキングの実装には&#x200B;**不要**&#x200B;です。メディアプレーヤー API を使用して、QoS とエラーの追跡に関連する変数を識別できます。

## プレーヤーイベント {#player-events}

### すべてのビットレート変更イベント時

* 再生の QoS オブジェクトインスタンス（`qosObject`）を作成または更新します
* を呼び出します `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### プレーヤーのエラー時

を呼び出します `trackError(“media error id”);`

## 実装方法 {#implement}

1. メディアの再生中にいつビットレートが変更されるかを識別し、QoS 情報を使用して `MediaObject` インスタンスを作成します。

   **QoSObject 変数：**

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

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
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。これにより、最も正確な QoS データを取得できます。

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します（[の概要](/help/sdk-implement/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
