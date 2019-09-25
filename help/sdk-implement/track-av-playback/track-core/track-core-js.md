---
seo-title: JavaScript でのコア再生の追跡
title: JavaScript でのコア再生の追跡
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JavaScript でのコア再生の追跡{#track-core-playback-on-javascript}

>[!IMPORTANT]
>このドキュメントでは、SDKバージョン2.xでのトラッキングについて説明します。 1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **初期トラッキングの設定**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | メディア名 | ○ |
   | `mediaid` | メディアの一意の識別子 | ○ |
   | `length` | メディアの長さ | ○ |
   | `streamType` | ストリームタイプ( _後述のStreamType定数_ ) | ○ |
   | `mediaType` | メディアタイプ( _以下のMediaType定数_ ) | ○ |

   **`StreamType`定数：**

   | 定数名 | 説明   |
   |---|---|
   | `VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `LIVE` | LIVE コンテンツのストリームタイプ。 |
   | `LINEAR` | LINEAR コンテンツのストリームタイプ。 |
   | `AOD` | Audio on Demandのストリームタイプ。 |
   | `AUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `PODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `Audio` | オーディオストリームのメディアタイプ。 |
   | `Video` | ビデオストリームのメディアタイプ。 |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **メタデータの添付**

   オプションで、コンテキストデータ変数を使用して、標準またはカスタムメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ**

      [JavaScript での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >標準メタデータオブジェクトのメディアオブジェクトへのアタッチはオプションです。

      * Media metadata keys API Reference - [Standard metadata keys - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **カスタムメタデータ**

      カスタム変数用の変数オブジェクトを作成し、このメディアのデータを設定します。 次に例を示します。

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **再生を開始する意図の追跡**

   メディアセッションの追跡を開始するには、Media Heartbeatイン `trackSessionStart` スタンスを呼び出します。

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >2つ目の値は、手順2で作成したカスタムメディアメタデータオブジェクト名です。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、データ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **再生の実際の開始の追跡**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **再生の完了の追跡**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **セッションの終了の追跡**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` トラッキングセッションの終わりを示します。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **すべての可能な一時停止シナリオの追跡**

   一時停止および呼び出しに関するイベントをメディアプレイヤーから識別しま `trackPause`す。

   ```js
   mediaHeartbeat.trackPause();
   ```

   **一時停止シナリオ**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリ*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリのセッションを開いたままにしておきたい。
   * （*モバイルアプリ*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からメディアを再開できるようにしたい。

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >これは、手順4で使用したのと同じイベントソースである場合があります。 Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* 追跡シナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー

