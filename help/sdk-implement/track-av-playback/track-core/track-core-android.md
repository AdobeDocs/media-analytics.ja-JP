---
title: Android でのコア再生の追跡
description: ここでは、AndroidでMedia SDKを使用してコアトラッキングを実装する方法について説明します。
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android でのコア再生の追跡{#track-core-playback-on-android}

>[!IMPORTANT]
>このドキュメントでは、SDKバージョン2.xでのトラッキングについて説明します。 1.x バージョンの SDK を実装する場合は、Android 向けの 1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **初期トラッキングの設定**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | メディア名 | ○ |
   | `mediaId` | メディアの一意の識別子 | ○ |
   | `length` | メディアの長さ | ○ |
   | `streamType` | ストリームタイプ( _後述のStreamType定数_ ) | ○ |
   | `mediaType` | メディアタイプ( _以下のMediaType定数_ ) | ○ |

   **`StreamType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `LIVE` | Live コンテンツのストリームタイプ。 |
   | `LINEAR` | Linear コンテンツのストリームタイプ。 |
   | `AOD` | オーディオオンデマンドのストリームタイプ。 |
   | `AUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `PODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `Audio` | オーディオストリームのメディアタイプ。 |
   | `Video` | ビデオストリームのメディアタイプ。 |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **メタデータの添付**

   オプションで、コンテキストデータ変数を使用して、標準またはカスタムメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ**

      [Android での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >標準メタデータオブジェクトのメディアオブジェクトへのアタッチはオプションです。

      * メディアメタデータキー API リファレンス - [標準メタデータキー - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * 利用可なビデオメタデータの包括的なセットについては、[オーディオおよびビデオパラメーター](/help/metrics-and-metadata/audio-video-parameters.md)を参照してください。
   * **カスタムメタデータ**

      カスタム変数用のディクショナリを作成し、このメディアのデータを設定します。 次に例を示します。

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **再生を開始する意図の追跡**

   メディアセッションの追跡を開始するには、Media Heartbeatイン `trackSessionStart` スタンスを呼び出します。 次に例を示します。

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >2つ目の値は、手順2で作成したカスタムメディアメタデータオブジェクト名です。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、メディアのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` () と `trackPlay` () の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **再生の実際の開始の追跡**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **再生の完了の追跡**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **セッションの終了の追跡**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` メディアトラッキングセッションの終わりを示します。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **すべての可能な一時停止シナリオの追跡**

   メディアの一時停止と呼び出しに関するイベントをメディアプレイヤーから識別しま `trackPause`す。

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **一時停止シナリオ**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリ*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリのセッションを開いたままにしておきたい。
   * （*モバイルアプリ*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からメディアを再開できるようにしたい。

1. 一時停止からのメディア再生およびメディア再開に関するイベントをメディアプレーヤーから識別し、`trackPlay` を呼び出します。

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >これは、手順4で使用したのと同じイベントソースである場合があります。 Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

コア再生の追跡に関する追加情報については、以下を参照してください。

* 追跡シナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Android SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー

