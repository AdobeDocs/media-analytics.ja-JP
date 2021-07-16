---
title: JavaScript 3.xを使用したQuality of Experienceの追跡について説明します。
description: 「JavaScript 3xを使用して、ブラウザーアプリでのメディアSDKを使用したQuality of Experience(QoE、QoS)追跡の実装について説明します。」
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 87%

---

# JavaScript 3.x を使用したエクスペリエンス品質の追跡{#track-quality-of-experience-on-javascript}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/sdk-implement/download-sdks.md)から開発者ガイドをダウンロードできます。

## QOE の実装

1. メディア再生中のビットレートの変化を識別し、QoE 情報を使用して `qoeObject` インスタンスを作成します。

   QoEObject の変数：

   >[!TIP]
   >
   >これらの変数は、QoS を追跡する場合にのみ必要です。

   | 変数 | タイプ | 説明 |
   | --- | --- | --- |
   | `bitrate` | 数値 | 現在のビットレート |
   | `startupTime` | 数値 | 起動時間 |
   | `fps` | 数値 | FPS の値 |
   | `droppedFrames` | 数値 | ドロップフレームの数 |

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
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します（[の概要](/help/sdk-implement/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
