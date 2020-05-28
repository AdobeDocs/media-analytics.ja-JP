---
title: JavaScript 3.xを使用したエクスペリエンスの質の追跡
description: このトピックでは、JavaScript 3xを使用するブラウザーアプリで、Media SDKを使用したエクスペリエンスの品質(QoE、QoS)トラッキングの実装について説明します。
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# JavaScript 3.xを使用したエクスペリエンスの質の追跡{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 3.x SDK に共通する実装のガイダンスです。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## QOEの実装

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   QoEObject変数：

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

   | 変数 | タイプ | 説明 |
   | --- | --- | --- |
   | `bitrate` | 数値 | 現在のビットレート |
   | `startupTime` | 数値 | 起動時間 |
   | `fps` | 数値 | FPS の値 |
   | `droppedFrames` | 数値 | ドロップフレームの数 |

   QoEオブジェクトの作成：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
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
   >QoEオブジェクトを更新し、ビットレートの変更ごとにビットレート変更イベントを呼び出します。 これにより、最も正確なQoEデータが提供されます。

1. SDKに最新のQoE情報を提供するために、必ず `updateQoEObject()` メソッドを呼び出してください。
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します（[の概要](/help/sdk-implement/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
