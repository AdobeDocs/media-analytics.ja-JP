---
title: コンテンツ再生のトラッキング
description: メディアの読み込み、開始、一時停止、完了などのトラッキングを含む、コア再生のトラッキングについて説明します。"
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# トラッキングの概要{#tracking-overview}

このドキュメントでは、バージョン 2.x の SDK でのトラッキングについて説明しています。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## プレーヤーイベント

コア再生のトラッキングには、メディアの読み込み、メディアの開始、メディアの一時停止およびメディアの完了のトラッキングが含まれます。また、必須ではありませんが、バッファーとシークのトラッキングもコンテンツ再生のトラッキングに使用されるコアコンポーネントです。ご使用のメディアプレーヤー API で、メディア SDK のトラッキングコールに対応するプレーヤーイベントを識別し、トラッキング API を呼び出すイベントハンドラーと、必須およびオプションの変数を設定するイベントハンドラーをコーディングします。

### メディアの読み込み時

* メディアオブジェクトを作成します
* メタデータを設定します
* `trackSessionStart` を呼び出します。例：`trackSessionStart(mediaObject, contextData)`

### メディアの開始時

* を呼び出します `trackPlay`

### 一時停止／再開時

* を呼び出します `trackPause`
* 再生が再開されたときに `trackPlay` を呼び出します。__

### メディアの完了時

* を呼び出します `trackComplete`

### メディアの中止時

* を呼び出します `trackSessionEnd`

### スクラビングの開始時

* を呼び出します `trackEvent(SeekStart)`

### スクラビングの終了時

* を呼び出します `trackEvent(SeekComplete)`
変更のキャンセル

### バッファリングの開始時

* を呼び出します `trackEvent(BufferStart);`

### バッファリングの終了時

* を呼び出します `trackEvent(BufferComplete);`

>[!TIP]
>
>再生ヘッドの位置は、セットアップおよび設定コードの一環として設定されます。`getCurrentPlayheadTime` について詳しくは、[概要：一般的な実装のガイドライン](/help/implementation/media-sdk-overview.md)を参照してください。


## 実装方法 {#implement}

1. **追跡の初期設定** - いつユーザーが再生の意図（ユーザーが再生をクリックする、または自動再生がオンになる）をトリガーするかを識別し、メディア情報（コンテンツ名、コンテンツ ID、コンテンツの長さ、ストリームのタイプ）を使用して `MediaObject` インスタンスを作成します。

   **`MediaObject`リファレンス：**

   | 変数名 | 説明 | 必須 |
   |---|---|---|
   | `name` | コンテンツ名 | ○ |
   | `mediaid` | コンテンツの一意の ID | ○ |
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

   `MediaObject` を作成するための一般的な形式は `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);` です。

1. **メタデータのアタッチ** - オプションで、コンテキストデータ変数を使用して標準またはカスタムのメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ -**

     >[!NOTE]
     >
     >メディアオブジェクトへの標準メタデータオブジェクトのアタッチはオプションです。

     標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。

     メタデータの包括的なリストについては、[オーディオおよびビデオパラメーター](../../implementation/variables/audio-video-parameters.md)を参照してください。

   * **カスタムメタデータ** - カスタム変数の変数オブジェクトを作成し、このコンテンツのデータを設定します。

1. **再生開始の意図を追跡** - セッションの追跡を開始するには、メディアハートビートインスタンスで `trackSessionStart` を呼び出します。

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。この API は、データ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >カスタムメタデータを使用しない場合は、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始をトラッキング** - 再生開始（コンテンツの最初のフレームが画面にレンダリングされる）に関するイベントをメディアプレーヤーから識別し、`trackPlay` を呼び出します。

1. **再生の完了をトラッキング** - 再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをメディアプレーヤーから識別し、`trackComplete` を呼び出します。

1. **セッションの終了をトラッキング** - 再生のアンロード／終了（ユーザーがコンテンツを閉じる、またはコンテンツが完了してアンロードされる）に関するイベントをメディアプレーヤーから識別し、`trackSessionEnd` を呼び出します。

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、トラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。`trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオをトラッキング** - 一時停止に関するイベントをメディアプレーヤーから識別し、`trackPause` を呼び出します。

   **一時停止のシナリオ** - プレーヤーが一時停止するあらゆるシナリオを識別し、`trackPause` が適切に呼び出されるようにします。以下のシナリオでは、アプリケーションで `trackPause()` を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からコンテンツを再開できるようにしたい。

1. 一時停止からの再生および再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   >[!TIP]
   >
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

1. メディアプレーヤーの再生シークイベントをリッスンします。シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。
1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。
1. メディアプレーヤーの再生バッファーイベントをリッスンし、バッファー開始イベント通知時に、`BufferStart` イベントを使用してバッファーを追跡します。
1. メディアプレーヤーからのバッファー完了通知時に、`BufferComplete` イベントを使用してバッファーの終わりを追跡します。

次のプラットフォーム固有のトピックに記載されている各手順の例と、SDK に含まれているサンプルプレーヤーを確認してください。

再生のトラッキングのシンプルな例については、次の HTML5 プレーヤーでの JavaScript 2.x SDK の使用を参照してください。

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
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## 検証 {#validate}

*レガシー*&#x200B;実装の検証について詳しくは、[レガシーの検証](/help/legacy/validation/validation-overview.md)を参照してください。
