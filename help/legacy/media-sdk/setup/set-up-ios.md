---
title: iOS で Media SDK をセットアップする方法
description: iOS で Media SDK アプリケーションをセットアップするには、次の手順に従います。
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/UP1biESuMpPqJNXKmEG-RU-8iBIHJcVZ87N0EsuZ1hI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 787
ht-degree: 88%

---

# iOS のセットアップ{#set-up-ios}

IOS デバイス用のストリーミングメディアサービスを設定する方法を説明します。

>[!IMPORTANT]
>
>2021 年 8 月 31 日（PT）にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。  詳しくは、[Media Analytics SDK のサポート終了に関する FAQ](/help/additional-resources/end-of-support-faqs.md) を参照してください。

## 前提条件

* **Media SDKの有効な設定パラメーターを取得する**
これらのパラメーターは、analytics アカウントを設定した後で、Adobe担当者から取得できます。
* **iOS用ADBMobileをアプリケーションに実装する**
Adobe Mobile SDKのドキュメントについて詳しくは、[iOS SDK 4.x for Experience Cloud Solutions](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=ja)を参照してください。

  >[!IMPORTANT]
  >
  >iOS 9 から、Apple は App Transport Security（ATS）という機能を導入しました。 この機能は、アプリケーションで業界標準のプロトコルと暗号のみを使用することで、ネットワークセキュリティの向上を目的としています。 この機能はデフォルトで有効になっていますが、ATS を利用する際の各種設定オプションが用意されています。 ATS について詳しくは、[App Transport Security](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=ja) を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**

   * _プレーヤーイベントをサブスクライブするための API_ - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * _プレーヤー情報を提供する API_ - メディア名や再生ヘッドなどの情報がこれに該当します。

## SDK の実装

>[!IMPORTANT]
>
>バージョン 2.3.0 以降、SDK は XCFrameworks を介して配布されます。
>
>SDK のバージョン 2.3.0 には Xcode 12.0 以降が必要で、該当する場合は Cocoapods 1.10.0 以降が必要です。

* バイナリライブラリファイルについて言及されている場合は常に、 XCFramework に置き換えて使用する必要があります。
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Adobe XCFrameworks を手動でプロジェクトに追加する場合は、埋め込まれていないことを確認してください。

1. [ダウンロードした](/help/getting-started/download-sdks.md)メディア SDK をプロジェクトに追加します。

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

      1. 「**[!UICONTROL Copy Items if Needed]**」チェックボックスが選択されていること、「**[!UICONTROL Create Groups]**」が選択されていること、および「**[!UICONTROL Add to Target]**」にあるチェックボックスが選択されていないことを確認します。

      ![オプションの選択](assets/choose-options_ios.png)

      1. 「**[!UICONTROL 完了]**」をクリックします。
      1. **[!UICONTROL Project Navigator]** で、アプリを選択し、ターゲットを選択します。
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

      1. アプリケーションがエラーなくビルドされることを確認します。

1. ライブラリをインポートします。

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. `ADBMediaHeartbeatConfig` インスタンスを作成します。

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

1. `ADBMediaHeartbeatDelegate` プロトコルを実装します。

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

1. `ADBMediaHeartBeatConfig` および `ADBMediaHeartBeatDelegate` を使用して、`ADBMediaHeartbeat` インスタンスを作成します。

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >`ADBMediaHeartbeat` インスタンスがアクセス可能であることと、*セッションの終わりまで解放されない*&#x200B;ことを確認します。 このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

## iOS でのバージョン 1.x から 2.x への移行 {#migrate-to-two-x}

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`ADBMediaHeartbeat` クラスに統合されています。 すべての設定は、`ADBMediaHeartbeatConfig` クラスに統合されています。

1.x から 2.x への移行について詳しくは、レガシー実装のドキュメントを参照してください。

## tvOS のネイティブアプリの設定

新しい Apple TV のリリースに伴い、ネイティブ tvOS 環境で実行するためのアプリケーションを作成できるようになりました。 iOS で利用可能ないくつかのフレームワークのいずれかを使用して完全にネイティブなアプリを作成するか、XML テンプレートおよび JavaScript を使用したアプリを作成できます。 MediaSDK バージョン 2.0 から、tvOS のサポートが利用できます。 tvOS について詳しくは、[tvOS Developer サイト](https://developer.apple.com/jp/tvos/)を参照してください。

次の手順を Xcode プロジェクトで実行します。 このガイドは、プロジェクトのターゲットの 1 つが tvOS をターゲティングした Apple TV アプリであることを想定して記述されています。

1. `VideoHeartbeat_TV.a` ライブラリファイルをプロジェクトの`lib` フォルダーにドラッグします。

1. tvOS アプリのターゲットの「**[!UICONTROL フェーズを作成]**」タブで、「**[!UICONTROL ライブラリとバイナリをリンク]**」セクションを展開し、次のライブラリを追加します。

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
