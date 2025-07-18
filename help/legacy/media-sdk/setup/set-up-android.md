---
title: Android で Media SDK をセットアップする方法
description: Android で Media SDK アプリケーションをセットアップするには、次の手順に従います。
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 97%

---

# Android のセットアップ{#set-up-android}

Android デバイス用の Streaming Media Collection の設定方法について説明します。

>[!IMPORTANT]
>
>2021 年 8 月 31 日（PT）にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。詳しくは、[Media Analytics SDK のサポート終了に関する FAQ](/help/additional-resources/end-of-support-faqs.md) を参照してください。


## 前提条件 

* **メディア SDK 用の有効な設定パラメーターを取得** これらのパラメーターは、Analytics アカウントの設定後、アドビの担当者から取得できます。
* **Android 向け ADBMobile をアプリケーションに実装** Adobe Mobile SDK ドキュメントについて詳しくは、[Experience Cloud ソリューション用 Android SDK 4.x](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=ja) を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**
   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

## SDK の実装

1. ダウンロードしたメディア SDK をプロジェクトに追加します。

   1. Android zip ファイル（例：`MediaSDK-android-v2.*.zip`）を展開します。
   1. `libs/` ディレクトリに `MediaSDK.jar` ファイルが存在することを確認します。

   1. プロジェクトにライブラリを追加します。

      **IntelliJ IDEA：**

      1. **[!UICONTROL プロジェクトナビゲーション]**&#x200B;パネルでプロジェクトを右クリックします。
      1. **[!UICONTROL モジュール設定を開く]**&#x200B;を選択します。
      1. **[!UICONTROL プロジェクト設定]**&#x200B;で、**[!UICONTROL ライブラリ]**&#x200B;を選択します。

      1. 「**[!UICONTROL +]**」をクリックして、新しいライブラリを追加します。
      1. 「**[!UICONTROL Java]**」を選択し、`MediaSDK.jar` ファイルに移動します。

      1. モバイルライブラリを使用する予定のモジュールを選択します。
      1. 「**[!UICONTROL 適用]**」をクリックしてから、「**[!UICONTROL OK]**」をクリックしてモジュール設定ウィンドウを閉じます。

      **Eclipse：**

      1. Eclipse IDE で、プロジェクト名を右クリックします。
      1. **[!UICONTROL ビルドパス]**／**[!UICONTROL 外部アーカイブの追加]**&#x200B;をクリックします。
      1. `MediaSDK.jar` を選択します。
      1. 「**[!UICONTROL 開く]**」をクリックします。
      1. プロジェクトを再度右クリックし、**[!UICONTROL ビルドパス]**／**[!UICONTROL ビルドパスを設定]**&#x200B;をクリックします。
      1. 「**[!UICONTROL 順序]**／**[!UICONTROL エクスポート]**」タブをクリックします。

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

1.x から 2.x への移行について詳しくは、レガシー実装のドキュメントを参照してください。
