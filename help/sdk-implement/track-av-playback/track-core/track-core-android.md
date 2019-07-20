---
seo-title: Android でのコア再生の追跡
title: Android でのコア再生の追跡
uuid: ab5fab95-76ed-4ae6- aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Android でのコア再生の追跡{#track-core-playback-on-android}

>[!IMPORTANT]
>このドキュメントでは、SDKのバージョン2. xのトラッキングについて説明します。1.x バージョンの SDK を実装する場合は、Android 向けの 1.x の開発ガイドをこちら（[SDK のダウンロード](../../../sdk-implement/download-sdks.md)）からダウンロードできます。

1. **初期トラッキングセットアップ**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | メディア名 | ○ |
   | `mediaId` | メディアの一意の識別子 | ○ |
   | `length` | メディアの長さ | ○ |
   | `streamType` | Stream type (see _StreamType constants_ below) | ○ |
   | `mediaType` | Media type (see _MediaType constants_ below) | ○ |

   **`StreamType`定数:**

   | 定数名 | 説明 |
   |---|---|
   | `VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `LIVE` | Live コンテンツのストリームタイプ。 |
   | `LINEAR` | Linear コンテンツのストリームタイプ。 |
   | `AOD` | オーディオオンデマンドのストリームタイプ。 |
   | `AUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `PODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数:**

   | 定数名 | 説明 |
   |---|---|
   | `Audio` | オーディオストリームのメディアタイプ。 |
   | `Video` | ビデオストリームのメディアタイプ。 |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **メタデータの添付**

   オプションで、コンテキストデータ変数を使用して、トラッキングセッションに標準またはカスタムのメタデータオブジェクトをアタッチします。

   * **標準メタデータ**

      [Android での標準メタデータの実装](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >標準のメタデータオブジェクトをメディアオブジェクトにアタッチすることはオプションです。

      * メディアメタデータキー API リファレンス - [標準メタデータキー - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * 利用可なビデオメタデータの包括的なセットについては、[オーディオおよびビデオパラメーター](../../../metrics-and-metadata/audio-video-parameters.md)を参照してください。
   * **カスタムメタデータ**

      カスタム変数用の辞書を作成し、このメディアのデータを入力します。次に例を示します。

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **再生を開始する意図を追跡する**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. 次に例を示します。

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >2番目の値は、手順2で作成したカスタムメディアメタデータオブジェクト名です。

   >[!IMPORTANT]
   >
   >`trackSessionStart` は、再生の開始ではなく、再生のユーザーの意図を追跡します。この API は、メディアのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` () と `trackPlay` () の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **実際の再生開始の追跡**

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

1. **セッションの終わりの追跡**

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
   >`trackSessionEnd` は、メディアトラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **すべての可能な一時停止シナリオの追跡**

   Identify the event from the media player for media pause and call `trackPause`:

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
   >これは、手順4で使用されていたイベントソースと同じです。Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

コア再生の追跡に関する追加情報については、以下を参照してください。

* 追跡シナリオ：[広告のない VOD 再生](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Android SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー

