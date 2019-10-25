---
seo-title: 追跡の概要
title: 追跡の概要
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 追跡の概要{#tracking-overview}

>[!IMPORTANT]
>
>このドキュメントでは、SDKバージョン2.xでのトラッキングについて説明します。 If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## プレイヤーイベント

コア再生の追跡には、メディアの読み込み、メディアの開始、メディアの一時停止およびメディアの完了の追跡が含まれます。また、必須ではありませんが、バッファーとシークの追跡もコンテンツ再生の追跡に使用されるコアコンポーネントです。ご使用のメディアプレーヤー API で、メディア SDK のトラッキングコールに対応するプレーヤーイベントを識別し、トラッキング API を呼び出すイベントハンドラーと、必須およびオプションの変数を設定するイベントハンドラーをコーディングします。

### メディアの読み込み時

* メディアオブジェクトを作成します
* メタデータを設定します
* 呼び `trackSessionStart`出し例： `trackSessionStart(mediaObject, contextData)`

### メディア開始時

* 呼び出し `trackPlay`

### 一時停止/再開時

* 呼び出し `trackPause`
* Call `trackPlay`   _when playback resumes_

### メディア完了時

* 呼び出し `trackComplete`

### メディアの中止時

* 呼び出し `trackSessionEnd`

### スクラブ開始時

* 呼び出し `trackEvent(SeekStart)`

### スクラブ終了時

* 呼び出し `trackEvent(SeekComplete)`

### バッファリング開始時

* 呼び出し `trackEvent(BufferStart);`

### バッファリングが終了した場合

* 呼び出し `trackEvent(BufferComplete);`

>[!TIP]
>
>再生ヘッドの位置は、設定および設定コードの一部として設定されます。 詳しくは、概要を参 `getCurrentPlayheadTime`照してく [ださい。一般的な導入のガイドラインを参照してください。](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## 実装方法 {#implement}

1. **追跡の初期設定** - いつユーザーが再生の意図（ユーザーが再生をクリックする、または自動再生がオンになる）をトリガーするかを識別し、メディア情報（コンテンツ名、コンテンツ ID、コンテンツの長さ、ストリームのタイプ）を使用して `MediaObject` インスタンスを作成します。

   **`MediaObject`参照：**

   | 変数名 | 説明 | 必須 |
   |---|---|---|
   | `name` | コンテンツ名 | ○ |
   | `mediaid` | コンテンツの一意の識別子 | ○ |
   | `length` | コンテンツの長さ | ○ |
   | `streamType` | ストリームタイプ | ○ |
   | `mediaType` | メディアタイプ（オーディオまたはビデオコンテンツ） | ○ |

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

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **メタデータのアタッチ** - オプションで、コンテキストデータ変数を使用して標準またはカスタムのメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ** -

      >[!NOTE]
      >
      >標準メタデータオブジェクトのメディアオブジェクトへのアタッチはオプションです。

      標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。

      See the comprehensive list of metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **カスタムメタデータ** - カスタム変数の変数オブジェクトを作成し、このコンテンツのデータを設定します。

1. **再生開始の意図を追跡** - セッションの追跡を開始するには、メディアハートビートインスタンスで `trackSessionStart` を呼び出します。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、データ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **実際の再生開始を追跡** - 再生開始（コンテンツの最初のフレームが画面にレンダリングされる）に関するイベントをメディアプレーヤーから識別し、`trackPlay` を呼び出します。

1. **再生の完了を追跡** - 再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをメディアプレーヤーから識別し、`trackComplete` を呼び出します。

1. **セッションの終了を追跡** - 再生のアンロード／終了（ユーザーがコンテンツを閉じる、またはコンテンツが完了してアンロードされる）に関するイベントをメディアプレーヤーから識別し、`trackSessionEnd` を呼び出します。

   >[!IMPORTANT]
   >
   >`trackSessionEnd` トラッキングセッションの終わりを示します。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **考えられるすべての一時停止シナリオを追跡** - 一時停止に関するイベントをメディアプレーヤーから識別し、`trackPause` を呼び出します。

   **一時停止のシナリオ** - プレーヤーが一時停止するあらゆるシナリオを識別し、`trackPause` が適切に呼び出されるようにします。以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリ*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリのセッションを開いたままにしておきたい。
   * （*モバイルアプリ*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からコンテンツを再開できるようにしたい。

1. 一時停止からの再生および再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   >[!TIP]
   >
   >これは、手順4で使用したのと同じイベントソースである場合があります。 Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. メディアプレーヤーの再生シークイベントをリッスンします。シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。
1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。
1. メディアプレーヤーの再生バッファーイベントをリッスンし、バッファー開始イベント通知時に、`BufferStart` イベントを使用してバッファーを追跡します。
1. メディアプレーヤーからのバッファー完了通知時に、`BufferComplete` イベントを使用してバッファーの終わりを追跡します。

次のプラットフォーム固有のトピックに記載されている各手順の例と、SDK に含まれているサンプルプレーヤーを確認してください。

再生の追跡のシンプルな例については、次の HTML5 プレーヤーでの JavaScript 2.x SDK の使用を参照してください。

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>, 
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## 検証 {#validate}

実装の検証について詳しくは、「検証」を参照して [ください。](/help/sdk-implement/validation/validation-overview.md)

