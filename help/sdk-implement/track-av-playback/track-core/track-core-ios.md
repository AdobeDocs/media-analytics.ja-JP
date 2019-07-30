---
seo-title: iOS でのコア再生の追跡
title: iOS でのコア再生の追跡
uuid: bdc0e05c-4fe5-430e- aee2- f331bc59ac6b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# iOS でのコア再生の追跡{#track-core-playback-on-ios}

>[!IMPORTANT]
>このドキュメントでは、SDKのバージョン2. xのトラッキングについて説明します。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **初期トラッキングセットアップ**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 変数名 | 説明 | 必須 |
   |---|---|---|
   | `name` | ビデオ名 | ○ |
   | `mediaid` | ビデオの一意の識別子 | ○ |
   | `length` | ビデオの長さ | ○ |
   | `streamType` | Stream type (see _StreamType constants_ below) | ○ |
   | `mediaType` | Media type (see _MediaType constants_ below) | ○ |

   **`StreamType`定数:**

   | 定数名 | 説明 |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | ビデオオンデマンドのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Live コンテンツのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Linear コンテンツのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeAOD` | オーディオオンデマンドのストリームタイプ。 |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `ADBMediaHeartbeatStreamTypePODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数:**

   | 定数名 | 説明 |
   |---|---|
   | `ADBMediaTypeAudio` | オーディオストリームのメディアタイプ。 |
   | `ADBMediaTypeVideo` | ビデオストリームのメディアタイプ。 |

   `MediaObject` を作成するための一般的な形式：

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **ビデオメタデータの添付**

   オプションで、コンテキストデータ変数を使用して、ビデオトラッキングセッションに標準ビデオまたはカスタムビデオメタデータオブジェクトをアタッチします。

   * **標準のビデオメタデータ**

      * [iOS での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **ビデオメタデータキー**
         [iOS のメタデータキー](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * ビデオメタデータの包括的なリストについては、[オーディオおよびビデオパラメーター](/help/metrics-and-metadata/audio-video-parameters.md)を参照してください。
      >[!NOTE]
      >
      >標準のビデオメタデータオブジェクトをメディアオブジェクトにアタッチすることはオプションです。

   * **カスタムメタデータ**

      カスタム変数の変数オブジェクトを作成し、このビデオのデータを入力します。次に例を示します。

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **再生を開始する意図を追跡する**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance.

   >[!TIP]
   >
   >2番目の値は、手順2で作成したカスタムビデオメタデータオブジェクト名です。

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` は、再生の開始ではなく、再生のユーザーの意図を追跡します。この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **実際の再生開始の追跡**

   ビデオの再生開始（ビデオの最初のフレームが画面に表示）に関するイベントをビデオプレーヤーから識別し、`trackPlay` () を呼び出します。

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **再生の完了の追跡**

   ビデオの再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをビデオプレーヤーから識別し、`trackComplete` () を呼び出します。

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **セッションの終わりの追跡**

   ビデオ再生のアンロード／終了（ユーザーがビデオを閉じる、またはビデオの再生が完了してアンロードされる）に関するイベントをビデオプレーヤーから識別し、`trackSessionEnd` () を呼び出します。

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、ビデオトラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **すべての可能な一時停止シナリオの追跡**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **一時停止シナリオ**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリ*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリのセッションを開いたままにしておきたい。
   * （*モバイルアプリ*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からビデオを再開できるようにしたい。

1. 一時停止からのビデオ再生およびビデオ再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >これは、手順4で使用されていたイベントソースと同じです。ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

コア再生の追跡に関する追加情報については、以下を参照してください。

* 追跡シナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* iOS SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー

