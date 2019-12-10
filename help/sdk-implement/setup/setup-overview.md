---
title: セットアップの概要
description: モバイル、OTT およびブラウザー（JS）アプリケーションでのメディアトラッキングのためのメディア SDK のセットアップの概要です。
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# セットアップの概要 {#setup-overview}

>[!IMPORTANT]
>
>以下の手順は、メディア SDK 2.x に適用されます。メディア SDK の 1.x バージョンを実装する場合は、[メディア SDK 1.x のドキュメントを参照してください。](/help/sdk-implement/download-sdks.md) Primetime のインテグレーターの場合は、後述の _Primetime メディア SDK のドキュメント_&#x200B;を参照してください。


## サポートされる最小プラットフォームバージョン {#minimum-platform-version}

次の表に、2019 年 2 月 19 日より各 SDK でサポートされている最小プラットフォームバージョンを示します。

| OS／ブラウザー | 必要な最小バージョン |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0 Lollipop 以降 |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般的な実装のガイドライン {#general-implementation-guidelines}

メディアトラッキングには、主に以下の 3 つの SDK コンポーネントが必要です。
* Media Heartbeat Config - この Config にはレポート用の基本設定が含まれます。
* Media Heartbeat Delegate - この Delegate は再生時間と QoS オブジェクトを制御します。
* Media Heartbeat - メンバーとメソッドを含むプライマリライブラリです。

次の実装手順を実行します。

1. `MediaHeartbeatConfig` インスタンスを作成し、設定パラメーター値を設定します。

   |  変数名  | 説明  | 必須 |  デフォルト値  |
   |---|---|:---:|---|
   | `trackingServer` | メディア分析用のトラッキングサーバー。これは、Analytics トラッキングサーバーとは異なります。 | ○ | 空の文字列 |
   | `channel` | チャネル名 | × | 空の文字列 |
   | `ovp` | コンテンツの配布に使用するオンラインメディアプラットフォームの名前。 | × | 空の文字列 |
   | `appVersion` | メディアプレーヤーアプリ／SDK のバージョン。 | × | 空の文字列 |
   | `playerName` | 使用中のビデオプレーヤーの名前（例："AVPlayer"、"HTML5 Player"、"My Custom Player"）。 | × | 空の文字列 |
   | `ssl` | 呼び出しが HTTPS を使用しておこなわれる必要があるかどうかを示します。 | × | false |
   | `debugLogging` | デバッグのログが有効になっているかどうかを示します。 | × | false |

1. `MediaHeartbeatDelegate` を実装します。

   |  メソッド名  |  説明  | 必須 |
   | --- | --- | :---: |
   | `getQoSObject()` | 現在の QoS 情報を含む `MediaObject` インスタンスを返します。このメソッドは、再生セッション中に複数回呼び出されます。プレーヤー実装は、常に、利用可能な最新の QoS データを返す必要があります。 | ○ |
   | `getCurrentPlaybackTime()` | 再生ヘッドの現在の位置を返します。VOD 追跡の場合は、メディアアイテムの開始時からの時間（秒）を返します。線形追跡またはライブ追跡の場合は、プログラムの開始時からの時間（秒）を返します。 | ○ |

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

## 検証{#validate}

Media Analytics 追跡実装は、2 つのタイプのトラッキングコールを生成します。

* メディア開始および広告開始の呼び出しは Adobe Analytics（AppMeasurement）サーバーに直接送信されます。
* ハートビート呼び出しは、Media Analytics（ハートビート）トラッキングサーバーに送信され、そこで処理されて、Adobe Analytics サーバーに渡されます。

* **Adobe Analytics（AppMeasurement）サーバー** トラッキングサーバーオプションについて詳しくは、[trackingServer および trackingServerSecure 変数の適切な設定](https://helpx.adobe.com/jp/analytics/kb/determining-data-center.html)を参照してください。

   >[!IMPORTANT]
   >
   >Experience Cloud 訪問者 ID サービスを使用するには、RDC トラッキングサーバーまたは RDC サーバーに解決される CNAME が必要です。

   Analytics トラッキングサーバーは「`.sc.omtrdc.net`」で終わるか CNAME である必要があります。

* ** Media Analytics（ハートビート）サーバー** これは、常に「`[your_namespace].hb.omtrdc.net`」形式になります。「`[your_namespace]`」の値は会社を指定し、アドビによって提供されます。

メディアトラッキングはあらゆるプラットフォーム、デスクトップ、モバイルで同じように動作します。オーディオトラッキングは、現在、モバイルプラットフォームで動作します。すべてのトラッキングコールに共通する、検証が必要な主要ユニバーサル変数がいくつかあります。

## SDK 1.x ドキュメント {#sdk-1x-documentation}

| Video Analytics 1.x SDK |  開発者ガイド（PDF のみ） |
| --- | --- |
| Android | [Android 向け設定 ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Apple TV 向け設定 ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast 向け設定 ](chromecast_1.x_sdk.pdf) |
| iOS | [iOS 向け設定 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript 向け設定 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android：   [Media Analytics の設定](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS：   [Media Analytics の設定](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS：   [Media Analytics の設定](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML 向け設定 ](vhl_tvml.pdf) |

## Primetime メディア SDK のドキュメント {#primetime-docs}

* [Primetime ユーザーガイド](https://helpx.adobe.com/jp/primetime/user-guide.html)
