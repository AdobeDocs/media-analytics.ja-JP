---
title: Chromecast でのコア再生の追跡
description: このトピックでは、ChromecastでのMedia SDKを使用したコアトラッキングの実装方法について説明します。
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast でのコア再生の追跡{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>このドキュメントでは、SDKバージョン2.xでのトラッキングについて説明します。 1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **初期トラッキングの設定**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`API リファレンス:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`定数：**

   [ADBMobileメディア](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`定数：**

   [ADBMobileメディア](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **ビデオメタデータの添付**

   オプションで、コンテキストデータ変数を使用して、標準またはカスタムビデオメタデータオブジェクトをビデオトラッキングセッションにアタッチします。

   * **標準のビデオメタデータ**

      [Chromecast での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >標準ビデオメタデータオブジェクトのメディアオブジェクトへのアタッチは任意です。

   * **カスタムメタデータ**

      カスタム変数用の変数オブジェクトを作成し、このビデオのデータを設定します。 次に例を示します。

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **再生を開始する意図の追跡**

   メディアセッションの追跡を開始するには、オブジェ [クトで](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) trackSessionStartを呼び出 `media` します。

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >2つ目の値は、手順2で作成したカスタムビデオメタデータオブジェクト名です。 If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **再生の実際の開始の追跡**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **再生の完了の追跡**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **セッションの終了の追跡**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` ビデオトラッキングセッションの終わりを示します。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **すべての可能な一時停止シナリオの追跡**

   Identify the event from the video player for video pause and call [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **一時停止シナリオ**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリ*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリのセッションを開いたままにしておきたい。
   * （*モバイルアプリ*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からビデオを再開できるようにしたい。

1. Identify the event from the player for video play and/or video resume from pause and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >これは、手順4で使用したのと同じイベントソースである場合があります。 ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* 追跡シナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Chromecast SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー

