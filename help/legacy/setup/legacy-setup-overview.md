---
title: レガシー Media SDK の実装の説明
description: モバイルアプリケーション、OTT アプリケーションおよびブラウザー（JS）アプリケーションでメディアトラッキング用に **レガシー** 2.x Media SDK をセットアップする方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
TQID: https://experienceleague.adobe.com/8wkHfEeGx3TtATwf9TH7B6exw2lV5xkgOm-z5GCqajQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 805
ht-degree: 87%

---

# レガシー 2.x Streaming Media SDK セットアップの概要{#setup-overview}

この節の手順は、**レガシー** 2.x Media SDK に適用されます。

* Media SDK の 1.x バージョンの実装について詳しくは、[1.x Media SDK のドキュメント](/help/getting-started/download-sdks.md)を参照してください。

* Primetime のインテグレーターの場合は、_Primetime Media SDK のドキュメント_&#x200B;を参照してください。

>[!IMPORTANT]
>
>2021 年 8 月 31 日（PT）にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。  詳しくは、[Media Analytics SDK のサポート終了に関する FAQ](/help/additional-resources/end-of-support-faqs.md) を参照してください。


## サポートされる最小プラットフォームバージョン {#minimum-platform-version}

次の表に、2019 年 2 月 19 日（PT）より各 SDK でサポートされている最小プラットフォームバージョンを示します。

| OS／ブラウザー | 必要な最小バージョン |
| --- | --- |
| iOS | iOS 6 以降 |
| Android | Android 5.0 Lollipop 以降 |
| Chrome | v22 以降 |
| Mozilla | v27 以降 |
| Safari | v7 以降 |
| IE | v11 以降 |

## 一般的な実装のガイドライン {#general-implementation-guidelines}

メディアトラッキングには、3 つの主な SDK コンポーネントが関与しています。
* メディアハートビート設定 - 設定には、レポートの基本設定が含まれています。
* メディアハートビートデリゲート - このデリゲートは再生時間と QoS オブジェクトを制御します。
* メディアハートビート - メンバーとメソッドを含むプライマリライブラリ。

次の実装手順を実行します。

1. `MediaHeartbeatConfig` インスタンスを作成し、設定パラメーター値を設定します。

   |  変数名  | 説明  | 必須 |  デフォルト値  |
   |---|---|:---:|---|
   | `trackingServer` | メディア分析用のトラッキングサーバー。 Analytics トラッキングサーバーとは異なります。 | ○ | 空の文字列 |
   | `channel` | チャネル名 | × | 空の文字列 |
   | `ovp` | コンテンツの配布に使用するオンラインメディアプラットフォームの名前。 | × | 空の文字列 |
   | `appVersion` | メディアプレーヤーアプリケーション／SDK のバージョン。 | × | 空の文字列 |
   | `playerName` | 使用中のメディアプレーヤーの名前（例：「AVPlayer」、「HTML5 Player」、「My Custom Player」）。 | × | 空の文字列 |
   | `ssl` | 呼び出しを HTTPS 経由でおこなう必要があるかどうかを示します。 | × | false |
   | `debugLogging` | デバッグのログが有効になっているかどうかを示します。 | × | false |

1. `MediaHeartbeatDelegate` を実装します。

   |  メソッド名  |  説明  | 必須 |
   | --- | --- | :---: |
   | `getQoSObject()` | 現在の QoS 情報を含む `MediaObject` インスタンスを返します。 このメソッドは、再生セッション中に複数回呼び出されます。 プレーヤー実装は、常に、利用可能な最新の QoS データを返す必要があります。 | ○ |
   | `getCurrentPlaybackTime()` | 再生ヘッドの現在の位置を返します。<br /> VOD トラッキングの場合、値はメディアアイテムの先頭から秒単位で指定されます。<br /> ライブストリーミングの場合、プレーヤーがコンテンツ時間に関する情報を提供しない場合、その日の午前0時UTCからの秒数として値を指定できます。<br /> メモ：プログレスマーカーを使用する場合、コンテンツのデュレーションが必要です。また、再生ヘッドはメディアアイテムの先頭からの（0 から始まる）秒数で更新する必要があります。 | ○ |

   >[!TIP]
   >
   >サービス品質（QoS）オブジェクトはオプションです。 プレーヤーで QoS データが使用可能であり、そのデータを追跡する場合は、以下の変数が必要です。

   | 変数名 | 説明   | 必須 |
   | --- | --- | :---: |
   | `bitrate` | ビット／秒（bps）単位のメディアのビットレート。 | ○ |
   | `startupTime` | メディアの起動時間（ミリ秒）。 | ○ |
   | `fps` | 1 秒あたりの表示フレーム数。 | ○ |
   | `droppedFrames` | それまでのドロップフレームの数。 | ○ |

1. `MediaHeartbeat` インスタンスを作成します。

   `MediaHertbeatConfig` および `MediaHertbeatDelegate` を使用して、`MediaHeartbeat` インスタンスを作成します。

   >[!IMPORTANT]
   >
   >`MediaHeartbeat` インスタンスがアクセス可能であることと、セッションの終わりまで解放されないことを確認します。 このインスタンスは、以下のすべてのメディアトラッキングイベントに使用されます。

   >[!TIP]
   >
   >`MediaHeartbeat` が Adobe Analytics に呼び出しを送信するためには、`AppMeasurement` のインスタンスが必要です。

1. すべての要素を組み合わせます。

   以下のサンプルコードでは HTML5 ビデオプレーヤー用の JavaScript 2.x SDK を使用しています。

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   
   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
   mediaConfig.playerName = "HTML5 Basic";
   mediaConfig.channel = "Video Channel";
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = "2.0";
   mediaConfig.ssl = false;
   mediaConfig.ovp = "";
   
   // Media Heartbeat Delegate
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Set mediaDelegate CurrentPlaybackTime
   mediaDelegate.getCurrentPlaybackTime = function() {
       return video.currentTime;
   };
   
   // Set mediaDelegate QoSObject - OPTIONAL
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes);
   }
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## 検証 {#validate}

Media Analytics トラッキング実装は、2 つのタイプのトラッキングコールを生成します。

* メディア開始および広告開始の呼び出しは Adobe Analytics（AppMeasurement）サーバーに直接送信されます。
* ハートビート呼び出しは、Media Analytics（ハートビート）トラッキングサーバーに送信され、そこで処理されて、Adobe Analytics サーバーに渡されます。

* **Adobe Analytics （AppMeasurement） サーバー**
トラッキングサーバーのオプションについて詳しくは、[trackingServerとtrackingServerSecureの変数を正しく設定するを参照してください。](https://helpx.adobe.com/jp/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Experience Cloud 訪問者 ID サービスを使用するには、RDC トラッキングサーバーまたは RDC サーバーに解決される CNAME が必要です。

  Analytics トラッキングサーバーは「`.sc.omtrdc.net`」で終わるか CNAME である必要があります。

* **&#x200B; Media Analytics （ハートビート）サーバー**
これには常に「`[your_namespace].hb.omtrdc.net`」という形式が使用されます。 「`[your_namespace]`」の値は会社を指定し、アドビによって提供されます。

メディアトラッキングはあらゆるプラットフォーム、デスクトップ、モバイルで同じように動作します。 オーディオトラッキングは、現在、モバイルプラットフォームで動作します。 すべてのトラッキングコールに共通する、検証が必要な主要ユニバーサル変数がいくつかあります。

## SDK 1.x ドキュメント {#sdk-1x-documentation}

| Video Analytics 1.x SDK  |  開発者ガイド（PDF のみ） |
| --- | --- |
| Android | [Android用に設定](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Apple TV用に設定](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast用に設定](chromecast_1.x_sdk.pdf) |
| iOS | [iOS用に設定](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript用に設定](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android： [Media Analytics の設定](https://helpx.adobe.com/jp/support/primetime.html) </li> <li> DHLS： [Media Analytics の設定](https://helpx.adobe.com/jp/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS： [Media Analytics の設定](https://helpx.adobe.com/jp/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML用に設定](vhl_tvml.pdf) |

## Primetime メディア SDK のドキュメント {#primetime-docs}

* [Primetime ユーザーガイド](https://helpx.adobe.com/jp/support/primetime.html)
