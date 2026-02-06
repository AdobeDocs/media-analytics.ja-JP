---
title: JavaScript 3.x を使用したエクスペリエンス品質のトラッキング
description: JavaScript 3x を使用するブラウザーアプリで Media SDKを使用してエクスペリエンス品質（QoE、QoS）のトラッキングを実装する方法を説明します。
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 90%

---

# JavaScript 3.x を使用したエクスペリエンス品質の追跡{#track-quality-of-experience-on-javascript}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/getting-started/download-sdks.md)から開発者ガイドをダウンロードできます。

## QOE の実装

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
1. メディアプレーヤーでエラーが生じ、エラーイベントをプレーヤー API で利用できる場合は、`trackError()` を使用してそのエラーの情報を取得します（[の概要](/help/use-cases/track-errors/track-errors-overview.md)を参照）。

   >[!TIP]
   >
   >メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError()` の呼び出しの後で `trackSessionEnd()` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
