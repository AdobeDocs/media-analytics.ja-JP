---
title: Media SDK の実装
description: モバイルアプリケーション、OTT アプリケーション、ブラウザー（JS）アプリケーションでメディアトラッキング用に Media SDKをセットアップする方法について説明します。
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 94%

---

# レガシー - Media SDK セットアップの概要 {#setup-overview}

ビデオアプリまたはプレーヤー用の Media SDK をダウンロードしたら、この節の情報に従って、Media SDK をセットアップして実装します。


## 一般的な実装のガイドライン {#general-implementation-guidelines}

ストリーミングメディアコレクションでのトラッキングに使用する主なSDK コンポーネントは 3 つあります。
* Media Heartbeat 設定 - `MediaHeartbeatConfig` には、レポートの基本設定が含まれています。
* Media Heartbeat デリゲート - `MediaHeartbeatDelegate` は、再生時間と QoS オブジェクトを制御します。
* Media Heartbeat - `MediaHeartbeat` は、メンバーとメソッドを含むプライマリライブラリです。

## Streaming Media SDK の実装

Streaming Media SDK をセットアップして使用するには、次の実装手順を実行します。

1. `MediaHeartbeatConfig` インスタンスを作成し、設定パラメーター値を設定します。

   |  変数名  | 説明  | 必須 |  デフォルト値  |
   |---|---|:---:|---|
   | `trackingServer` | メディア分析用のトラッキングサーバー。Analytics トラッキングサーバーとは異なります。 | ○ | 空の文字列 |
   | `channel` | チャネル名 | × | 空の文字列 |
   | `ovp` | コンテンツの配布に使用するオンラインメディアプラットフォームの名前。 | × | 空の文字列 |
   | `appVersion` | メディアプレーヤーアプリケーション／SDK のバージョン。 | × | 空の文字列 |
   | `playerName` | 使用中のメディアプレーヤーの名前（例：「AVPlayer」、「HTML5 Player」、「My Custom Player」）。 | × | 空の文字列 |
   | `ssl` | 呼び出しを HTTPS 経由でおこなう必要があるかどうかを示します。 | × | false |
   | `debugLogging` | デバッグのログが有効になっているかどうかを示します。 | × | false |

1. `MediaHeartbeatDelegate` を実装します。

   |  メソッド名  |  説明  | 必須 |
   | --- | --- | :---: |
   | `getQoSObject()` | 現在の QoS 情報を含む `MediaObject` インスタンスを返します。このメソッドは、再生セッション中に複数回呼び出されます。プレーヤー実装は、常に、利用可能な最新の QoS データを返す必要があります。 | ○ |
   | `getCurrentPlaybackTime()` | 再生ヘッドの現在の位置を返します。<br /> VOD トラッキングの場合、メディアアイテムの先頭からの秒数で指定します。<br /> ライブストリーミングでは、プレーヤーがコンテンツのデュレーションに関する情報を提供しない場合、その日の午前0時（UTC）からの秒数を指定できます。 <br /> メモ：プログレスマーカーを使用する場合、コンテンツのデュレーションが必要であり、再生ヘッドはメディアアイテムの先頭から、0 から始まる秒数で更新する必要があります。 | ○ |

   >[!TIP]
   >
   >サービス品質（QoS）オブジェクトはオプションです。プレーヤーで QoS データが使用可能であり、そのデータを追跡する場合は、以下の変数が必要です。

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
   >`MediaHeartbeat` インスタンスがアクセス可能であることと、セッションの終わりまで解放されないことを確認します。このインスタンスは、以下のすべてのメディアトラッキングイベントに使用されます。

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

* **Adobe Analytics（AppMeasurement）サーバー** トラッキングサーバーオプションについて詳しくは、[trackingServer および trackingServerSecure 変数の適切な設定](https://helpx.adobe.com/jp/analytics/kb/determining-data-center.html)を参照してください。

  >[!IMPORTANT]
  >
  >Experience Cloud 訪問者 ID サービスを使用するには、RDC トラッキングサーバーまたは RDC サーバーに解決される CNAME が必要です。

  Analytics トラッキングサーバーは「`.sc.omtrdc.net`」で終わるか CNAME である必要があります。

* ** Media Analytics（ハートビート）サーバー** これは、常に「`[your_namespace].hb.omtrdc.net`」形式になります。「`[your_namespace]`」の値は会社を指定し、アドビによって提供されます。

メディアトラッキングはあらゆるプラットフォーム、デスクトップ、モバイルで同じように動作します。オーディオトラッキングは、現在、モバイルプラットフォームで動作します。すべてのトラッキングコールに共通する、検証が必要な主要ユニバーサル変数がいくつかあります。
