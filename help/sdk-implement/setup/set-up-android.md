---
seo-title: Android のセットアップ
title: Android のセットアップ
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Android のセットアップ{#set-up-android}

## 前提条件

* **Media SDKの有効な設定パラメーターの取得** Analyticsアカウントを設定した後で、これらのパラメーターをアドビの担当者から取得できます。
* **アプリケーションにAndroid用ADBMobileを実装** Adobe Mobile SDKドキュメントについて詳しくは、 [Experience cloudソリューション用Android SDK 4.xを参照してください。](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **メディアプレーヤーで以下の機能を設定します。**
   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

## SDK の実装

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-2x-sdks)メディア SDK をプロジェクトに追加します。

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. プロジェクトにライブラリを追加します。

      **IntelliJ IDEA：**

      1. **[!UICONTROL プロジェクトナビゲーション]**&#x200B;パネルでプロジェクトを右クリックします。
      1. 「**[!UICONTROL モジュール設定を開く]**」を選択します。
      1. 「**[!UICONTROL プロジェクト設定]**」で、「**[!UICONTROL ライブラリ]**」を選択します。

      1. Click **[!UICONTROL +]** to add a new library.
      1. 「**[!UICONTROL Java]**」を選択し、`MediaSDK.jar` ファイルに移動します。

      1. モバイルライブラリを使用する予定のモジュールを選択します。
      1. 「**[!UICONTROL 適用]**」をクリックしてから、「**[!UICONTROL OK]**」をクリックしてモジュール設定ウィンドウを閉じます。
      **Eclipse：**

      1. Eclipse IDE で、プロジェクト名を右クリックします。
      1. **[!UICONTROL Build Path（ビルドパス）]**／**[!UICONTROL Add External Archives（外部アーカイブの追加）]**&#x200B;をクリックします。
      1. Select `MediaSDK.jar`.
      1. 「**[!UICONTROL Open（開く）]**」をクリックします。
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. 「**[!UICONTROL 順序]**／**[!UICONTROL エクスポート]**」タブをクリックします。

      1. `MediaSDK.jar` ファイルが選択されていることを確認します。


1. ライブラリをインポートします。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

**アプリの権限の追加**

メディア SDK を使用するアプリでは、トラッキングコールでデータを送信するために以下の権限が必要です。

* `INTERNET`
* `ACCESS_NETWORK_STATE`

これらの権限を追加するには、アプリケーションのプロジェクトディレクトリにある `AndroidManifest.xml` ファイルに以下の行を追加します。

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Android でのバージョン 1.x から 2.x への移行**

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`com.adobe.primetime.va.simple.MediaHeartbeat` クラスに統合されています。また、すべての設定は、`com.adobe.primetime.va.simple.MediaHeartbeatConfig` クラスに統合されました。

1.xから2.xへの移行について詳しくは、 [mig-1x-2x-overview.mdを参照してください。](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
