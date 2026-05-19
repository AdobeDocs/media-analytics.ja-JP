---
title: Media SDK の実装
description: モバイル、OTT、およびブラウザー（JS）アプリケーションでMedia SDKをメディアトラッキング用に設定する方法について説明します。
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/DsVDPsePWd123v5D8OdC2zUn52IWAOwh6QxcpvB1FIs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
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
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 626
ht-degree: 81%

---

# レガシー - Media SDK セットアップの概要 {#setup-overview}

ビデオアプリまたはプレーヤー用の Media SDK をダウンロードしたら、この節の情報に従って、Media SDK をセットアップして実装します。


## 一般的な実装のガイドライン {#general-implementation-guidelines}

ストリーミングメディアサービスでのトラッキングで使用されるSDKには、主に3つのコンポーネントがあります。
* Media Heartbeat 設定 - `MediaHeartbeatConfig` には、レポートの基本設定が含まれています。
* Media Heartbeat デリゲート - `MediaHeartbeatDelegate` は、再生時間と QoS オブジェクトを制御します。
* Media Heartbeat - `MediaHeartbeat` は、メンバーとメソッドを含むプライマリライブラリです。

## Streaming Media SDK の実装

Streaming Media SDK をセットアップして使用するには、次の実装手順を実行します。

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
