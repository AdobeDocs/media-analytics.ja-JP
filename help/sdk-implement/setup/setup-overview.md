---
seo-title: セットアップの概要
title: セットアップの概要
uuid: 06ffeeddb- b0c8-4f7d-90c8- e374cde1695
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>次の手順は、2. xメディアSDKに適用されます。メディア SDK の 1.x バージョンを実装する場合は、[メディア SDK 1.x のドキュメントを参照してください。](../download-sdks.md) Primetimeインテグレーターについては、以下の _Primetime Media SDKドキュメント_ を参照してください。


## Minimum Platform Version Support {#minimum-platform-version}

次の表に、2019年2月20日からの各SDKでサポートされる最小プラットフォームバージョンを示します。

| OS/ブラウザー | 最小バージョンが必要です |
| --- | --- |
| iOS   | iOS 6+ |
| Android | Android5.0+- Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般的な実装のガイドライン {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

メディアトラッキングには、主に以下の 3 つの SDK コンポーネントが必要です。
* Media Heartbeat Config - この Config にはレポート用の基本設定が含まれます。
* Media Heartbeat Delegate - この Delegate は再生時間と QoS オブジェクトを制御します。
* Media Heartbeat - メンバーとメソッドを含むプライマリライブラリです。

次の実装手順を実行します。

1. `MediaHeartbeatConfig` インスタンスを作成し、configパラメーターの値を設定します。

   |  変数名  | 説明  | 必須 |  デフォルト値  |
   |---|---|:---:|---|
   | `trackingServer` | メディア分析用のトラッキングサーバー。これは、Analytics トラッキングサーバーとは異なります。 | ○ | 空の文字列 |
   | `channel` | チャネル名 | × | 空の文字列 |
   | `ovp` | コンテンツの配布に使用するオンラインメディアプラットフォームの名前。 | × | 空の文字列 |
   | `appVersion` | メディアプレーヤーアプリ／SDK のバージョン。 | × | 空の文字列 |
   | `playerName` | 使用中のビデオプレーヤーの名前（例："AVPlayer"、"HTML5 Player"、"My Custom Player"）。 | × | 空の文字列 |
   | `ssl` | 呼び出しが HTTPS を使用しておこなわれる必要があるかどうかを示します。 | × | false |
   | `debugLogging` | デバッグのログが有効になっているかどうかを示します。 | × | false |

1. Implement the `MediaHeartbeatDelegate`.

   |  メソッド名  |  説明  | 必須 |
   | --- | --- | :---: |
   | `getQoSObject()` | 現在の QoS 情報を含む `MediaObject` インスタンスを返します。このメソッドは、再生セッション中に複数回呼び出されます。プレーヤー実装は、常に、利用可能な最新の QoS データを返す必要があります。 | ○ |
   | `getCurrentPlaybackTime()` | 再生ヘッドの現在の位置を返します。VOD 追跡の場合は、メディアアイテムの開始時からの時間（秒）を返します。線形追跡またはライブ追跡の場合は、プログラムの開始時からの時間（秒）を返します。 | ○ |

   >[!TIP]
   >
   >Quality of Service（QoS）オブジェクトはオプションです。プレーヤーで QoS データが使用可能であり、そのデータを追跡する場合は、以下の変数が必要です。

   | 変数名 | 説明   | 必須 |
   | --- | --- | :---: |
   | `bitrate` | ビット／秒（bps）単位のメディアのビットレート。 | ○ |
   | `startupTime` | メディアの起動時間（ミリ秒）。 | ○ |
   | `fps` | 1 秒あたりの表示フレーム数。 | ○ |
   | `droppedFrames` | それまでのドロップフレームの数。 | ○ |

1. `MediaHeartbeat` インスタンスを作成します。

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. このインスタンスは、以下のすべてのメディアトラッキングイベントに使用されます。

   >[!TIP]
   >
   >`MediaHeartbeat` には、Adobe `AppMeasurement` Analyticsに呼び出しを送信するためのインスタンスが必要です。

1. すべての要素を組み合わせます。

   以下のサンプルコードでは HTML5 ビデオプレーヤー用の JavaScript 2.x SDK を使用しています。

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
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

## 検証 {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

メディア実装は以下の 2 つのタイプのトラッキングコールで構成されています。

* メディア開始および広告開始の呼び出しは AppMeasurement サーバーに直接送信されます。
* ハートビート呼び出しは、開始時、コンテンツの場合は 10 秒ごと、広告の場合は 1 秒ごとにハートビートトラッキングサーバーに送信されます。

メディアトラッキングはあらゆるプラットフォーム、デスクトップ、モバイルで同じように動作します。オーディオトラッキングは現在モバイルプラットフォームで動作します。すべてのトラッキングコールに共通する、検証が必要な主要ユニバーサル変数がいくつかあります。

* **AppMeasurement（Analytics）**&#x200B;サーバーオプションの詳細については、trackingServer変数とtrackingServerSecure変数の [適切な設定を参照してください。](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience Cloud訪問者IDサービスにはRDCサーバーへのRDCトラッキングサーバーまたはCNAME解決が必要です。

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* **ハートビート（Media Analytics）**&#x200B;には常に形式があります。`[namespace].hb.omtrdc.net`「ここで」`[namespace]`は、ログイン会社によって定義され、アドビが提供します。

## SDK 1.x Documentation {#section_acj_tkk_t2b}

| ビデオ分析1. x SDK | 開発者ガイド（PDFのみ） |
| --- | --- |
| Android | [Android 向け設定 ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Apple TV 向け設定 ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast 向け設定 ](chromecast_1.x_sdk.pdf) |
| iOS   | [iOS 向け設定 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript 向け設定 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML 向け設定 ](vhl_tvml.pdf) |

## Primetime メディア SDK のドキュメント {#primetime-docs}

* [Primetimeユーザーガイド](https://helpx.adobe.com/primetime/user-guide.html)
