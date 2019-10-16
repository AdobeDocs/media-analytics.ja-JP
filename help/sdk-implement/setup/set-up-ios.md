---
seo-title: iOS のセットアップ
title: iOS のセットアップ
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: f745d64c9cf843ef7237ee3c3c96c63d7edbc1c2

---


# iOS のセットアップ{#set-up-ios}

## 前提条件

* **Media SDKの有効な設定パラメーターの取得** Analyticsアカウントを設定した後で、これらのパラメーターをアドビの担当者から取得できます。
* **アプリケーションにiOS用ADBMobileを実装**&#x200B;します。Adobe Mobile SDKドキュメントについて詳しくは、 [iOS SDK 4.x for Experience Cloud Solutionsを参照してください。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >iOS 9以降、AppleはApp Transport Security(ATS)と呼ばれる機能を導入しました。 これはアプリで使用するプロトコルや暗号を業界標準のものに制限することで、ネットワークセキュリティを改善するための機能です。この機能はデフォルトで有効になっていますが、ATS を利用する際の各種設定オプションが用意されています。ATSについて詳しくは、「アプリ転送セキュリティ」 [を参照してください。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **メディアプレーヤーで以下の機能を設定します。**

   * _プレーヤーイベントをサブスクライブするための API_ - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * _プレーヤー情報を提供する API_ - メディア名や再生ヘッドなどの情報がこれに該当します。

## SDK の実装

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)メディア SDK をプロジェクトに追加します。

   1. `libs` ディレクトリに以下のソフトウェアコンポーネントが存在することを確認します。

      * `ADBMediaHeartbeat.h`：iOS ハートビートトラッキング API で使用される Objective-C ヘッダーファイル。
      * `ADBMediaHeartbeatConfig.h`：SDK 設定用の Objective-C ヘッダーファイル。
      * `MediaSDK.a`：iOS デバイス用のライブラリビルド（armv7、armv7s、arm64）とシミュレーター（i386 および x86_64）を含む、ビットコード対応の大きなバイナリ。

         ターゲットが iOS アプリを対象としている場合は、このバイナリがリンクされている必要があります。

      * `MediaSDK_TV.a`：新しい Apple TV デバイス用のライブラリビルド（arm64）とシミュレーター（x86_64）を含む、ビットコード対応の大きなバイナリ。

         このバイナリは、ターゲットが Apple TV（tvOS）アプリを対象としている場合、リンクされている必要があります。
   1. 以下のようにして、プロジェクトにライブラリを追加します。

      1. Xcode IDE を起動して、アプリを開きます。
      1. **[!UICONTROL Project Navigator]** で、`libs` ディレクトリをドラッグして、プロジェクトにドロップします。

      1. 「**[!UICONTROL Copy Items if Needed]**」チェックボックスが選択されていること、「**[!UICONTROL Create Groups]」が選択されていること、および「** Add to Target **」にあるチェックボックスが選択されていないことを確認します。**

         ![](assets/choose-options_ios.png)

      1. Click **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. 「**[!UICONTROL 一般]**」タブの「**[!UICONTROL リンクされたフレームワーク]**」および「**[!UICONTROL ライブラリ]**」セクションで、必要なフレームワークとライブラリをリンクさせます。

         **iOS アプリのターゲット：**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV（tvOS）のターゲット：**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. アプリがエラーなくビルドされることを確認します。




1. ライブラリをインポートします。

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   ここでは、`MediaHeartbeat` 設定パラメーターと、正確な追跡のために `MediaHeartbeat` インスタンスに正しい設定値を設定する方法を説明します。

   `ADBMediaHeartbeatConfig` 初期化のサンプル：

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

## iOS でのバージョン 1.x から 2.x への移行 {#migrate-to-two-x}

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`ADBMediaHeartbeat` クラスに統合されています。すべての設定は、`ADBMediaHeartbeatConfig` クラスに統合されています。

For more information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## tvOS のネイティブアプリの設定

新しい Apple TV のリリースに伴い、ネイティブ tvOS 環境で実行するためのアプリケーションを作成できるようになりました。iOS で利用可能ないくつかのフレームワークのいずれかを使用して完全にネイティブなアプリを作成するか、XML テンプレートおよび JavaScript を使用したアプリを作成できます。MediaSDK バージョン 2.0 から、tvOS のサポートが利用できます。For more information about tvOS, see [tvOS Developer site.](https://developer.apple.com/tvos/)

次の手順を Xcode プロジェクトで実行します。このガイドは、プロジェクトのターゲットの 1 つが tvOS 用の Apple TV アプリであることを想定して記述されています。

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. tvOS アプリのターゲットの「**[!UICONTROL Build Phases（ビルドフェーズ）]**」タブで、「**[!UICONTROL Link Binary with Libraries（バイナリをライブラリとリンク）]**」を展開して、以下のライブラリを追加します。

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

