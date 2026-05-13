---
title: Chromecast でエクスペリエンス品質をトラッキングする方法
description: ChromecastでMedia SDKを使用したエクスペリエンスの品質（QoE、QoS）トラッキングの実装について説明します。
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VR-udMMg3tOMsbxnt-f0zjkGVZNgnCON0diYrhhMuoE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 95%

---

# Chromecast でのエクスペリエンス品質の追跡{#track-quality-of-experience-on-chromecast}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## 概要 {#overview}

Quality of Experience の追跡には、サービス品質（QoS）およびエラー追跡が含まれますが、どちらもオプションの要素で、コアメディアトラッキングの実装には&#x200B;**不要**&#x200B;です。 メディアプレーヤー API を使用して、QoS とエラーの追跡に関連する変数を識別できます。

## プレーヤーイベント {#player-events}

### すべてのビットレート変更イベント時

* 再生の QoS オブジェクトインスタンス（`qosObject`）を作成または更新します
* を呼び出します `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### プレーヤーのエラー時

を呼び出します `trackError("media error id");`

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
   >ビットレートが変更されるたびに、QoS オブジェクトを更新し、ビットレート変更イベントを呼び出します。 これにより、最も正確な QoS データを取得できます。

1. `getQoSObject()` メソッドで、最新の QoS 情報が返されるようにします。
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します （[の概要](/help/use-cases/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。 メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
