---
title: JavaScript 3.x を使用したエクスペリエンス品質のトラッキング
description: JavaScript 3xを使用したブラウザーアプリでMedia SDKを使用したエクスペリエンスの質（QoE、QoS）トラッキングの実装について説明します。
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/aR7oVHv3n2xQnrMGHowhLFCYxhRyP1vyIrlXbKHEa5A
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 90%

---

# JavaScript 3.x を使用したエクスペリエンス品質の追跡{#track-quality-of-experience-on-javascript}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/getting-started/download-sdks.md)から開発者ガイドをダウンロードできます。

## QOEの実装

1. メディア再生中のビットレートの変化を識別し、QoE 情報を使用して `qoeObject` インスタンスを作成します。

   QoEObject の変数：

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

   | 変数 | タイプ | 説明 |
   | --- | --- | --- |
   | `bitrate` | number | 現在のビットレート |
   | `startupTime` | number | 起動時間 |
   | `fps` | number | FPS の値 |
   | `droppedFrames` | number | ドロップフレームの数 |

   QoE オブジェクトの作成：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. 再生中にビットレートが切り替わったときに、メディアハートビートインスタンスで `BitrateChange` イベントを呼び出します。

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >ビットレートが変更されるたびに、QoE オブジェクトを更新し、ビットレート変更イベントを呼び出します。 これにより、最も正確な QoE データを取得できます。

1. 必ず `updateQoEObject()` メソッドを呼び出して、最新の QoE 情報を SDK に提供してください。
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します （[の概要](/help/use-cases/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。 メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
