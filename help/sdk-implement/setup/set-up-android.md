---
title: Android のセットアップ
description: Android での実装用のメディア SDK アプリケーション設定です。
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# Android のセットアップ {#set-up-android}

>[!IMPORTANT]
>
>2020年10月より、アドビは、バージョン4のモバイルSDKと、スタンドアロンのMedia Analytics SDK for Androidのサポートを終了します。 バージョン4のSDKは引き続きダウンロードして使用できますが、カスタマーケアのサポートとフォーラムへのアクセスは終了します。 Android向けAdobe Experience Platform(AEP)SDKに移行する必要があります。 AEP Mobile SDK（旧称v5）は、Adobe Experience Cloudの機能のみをサポートします。 この変更について詳しくは、 [バージョン4モバイルSDKのサポート終了に関するFAQを参照してください](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)。 新しいAEP Mobile SDKに移行することをお勧めします。
AEP Mobile SDKに移行した後、Adobe Analyticsのオーディオとビデオに対して有効にするには、Analytics Launch拡張機能とMedia Analytics Launch拡張機能を実装する必要があります。 新しいAEP Mobile SDKへの移行について詳しくは、「スタンドアロンメディアSDKからAdobe Launchへの [移行」を参照してください。 ](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)


## 前提条件


* **メディア SDK 用の有効な設定パラメーターを取得** これらのパラメーターは、Analytics アカウントの設定後、アドビの担当者から取得できます。
* **Android 向け ADBMobile をアプリケーションに実装** Adobe Mobile SDK ドキュメントについて詳しくは、[Experience Cloud ソリューション用 Android SDK 4.x](https://docs.adobe.com/content/help/ja-JP/mobile-services/android/overview.html) を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**
   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

## SDK の実装

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-2x-sdks)メディア SDK をプロジェクトに追加します。

   1. Android zip ファイル（例：`MediaSDK-android-v2.*.zip`）を展開します。
   1. `libs/` ディレクトリに `MediaSDK.jar` ファイルが存在することを確認します。

   1. プロジェクトにライブラリを追加します。

      **IntelliJ IDEA：**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. **[!UICONTROL Open Module Settings]** を選択します。
      1. の下 **[!UICONTROL Project Settings]**&#x200B;でを選択し **[!UICONTROL Libraries]**&#x200B;ます。

      1. Click **[!UICONTROL +]** to add a new library.
      1. 「**[!UICONTROL Java]**」を選択し、`MediaSDK.jar` ファイルに移動します。

      1. モバイルライブラリを使用する予定のモジュールを選択します。
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse：**

      1. Eclipse IDE で、プロジェクト名を右クリックします。
      1. クリック  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. `MediaSDK.jar` を選択します。
      1. クリック **[!UICONTROL Open]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Click the **[!UICONTROL Order]** and **[!UICONTROL Export]** tabs.

      1. `MediaSDK.jar` ファイルが選択されていることを確認します。


1. ライブラリをインポートします。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. `MediaHeartbeatConfig` インスタンスを作成します。

   `MediaHeartbeatConfig` 初期化のサンプル：

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. `MediaHeartbeatDelegate` インターフェイスを実装します。

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. `MediaHeartbeat` インスタンスを作成します。

   `MediaHeartbeatConfig` インスタンスと `MediaHertbeatDelegate` インスタンスを使用して、`MediaHeartbeat` インスタンスを作成します。

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >`MediaHeartbeat` インスタンスがアクセス可能であることと、*セッションの終わりまで解放されない*&#x200B;ことを確認します。このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

**アプリの権限の追加**

メディア SDK を使用するアプリケーションでは、トラッキングコールでデータを送信するために以下の権限が必要です。

* `INTERNET`
* `ACCESS_NETWORK_STATE`

これらの権限を追加するには、アプリケーションのプロジェクトディレクトリにある `AndroidManifest.xml` ファイルに以下の行を追加します。

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Android でのバージョン 1.x から 2.x への移行**

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`com.adobe.primetime.va.simple.MediaHeartbeat` クラスに統合されています。また、すべての設定は、`com.adobe.primetime.va.simple.MediaHeartbeatConfig` クラスに統合されました。

1.x から 2.x への移行について詳しくは、[mig-1x-2x-overview.md](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md) を参照してください。
