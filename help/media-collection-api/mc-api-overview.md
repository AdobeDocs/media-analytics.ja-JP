---
title: 概要
description: null
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 概要{#overview}

メディアコレクション API は、クライアント側のメディア SDK の代替として使用できるアドビの RESTful API です。メディアコレクション API を使用すると、プレーヤーで RESTful HTTP 呼び出しを使用してオーディオおよびビデオイベントを追跡できます。Media Collection APIは、Media SDKと同じリアルタイムトラッキングに加え、1つの追加機能を提供します。

* **ダウンロードされたコンテンツの追跡**

   この機能を使用すると、ユーザーのデバイスがオンラインに戻るまで、イベントデータをローカルに保存して、ユーザーがオフラインの間にメディアを追跡できます。 （詳しくは、[ダウンロードされたコンテンツの追跡](track-downloaded-content.md)を参照してください）。

メディアコレクション API は、基本的に、メディア SDK のサーバー側バージョンとして動作するアダプターです。つまり、Media SDKドキュメントの一部の側面もMedia Collection APIに関連しています。 例えば、両方のソリューションで同じオーディオ [とビデオのパラメーターが使用され](/help/metrics-and-metadata/audio-video-parameters.md)、収集されたオーディオとビデオのトラッキングデータが同じレポートと分析 [に結び付きます。](/help/media-reports/media-reports-enable.md)

## メディアトラッキングデータのフロー {#media-tracking-data-flows}

メディアコレクションAPIを実装するメディアプレイヤーは、RESTful APIトラッキングコールをメディアトラッキングバックエンドサーバーに直接送信しますが、Media SDKを実装するプレイヤーは、プレーヤーアプリ内のSDK APIに対してトラッキングコールを送信します。 Web 経由で呼び出しを送信する影響の 1 つとして、メディアコレクション API を実装するプレーヤーでは、メディア SDK が自動的に処理する処理の一部を処理する必要があります(メディアコレク [ションの導入の詳細](mc-api-impl/mc-api-quick-start.md))。

Media Collection APIでキャプチャされたトラッキングデータは、Media SDKプレイヤーでキャプチャされたトラッキングデータとは異なる方法で送信され、最初に処理されますが、両方のソリューションでバックエンドの同じ処理エンジンが使用されます。

![](assets/col_api_overview_simple.png)

## APIの概要 {#api-overview}

**URI：**&#x200B;この情報はアドビの担当者から入手します。

**HTTP メソッド：** JSON リクエスト本文を使用した POST。

### API Calls {#mc-api-calls}

* **`sessions`— サー** バとのセッションを確立し、後続の呼び出しで使用されるセッションIDを返し `events` ます。 アプリは、トラッキングセッションの開始時にこれを 1 回呼び出します。

   ```
   {uri}/api/v1/sessions
   ```

* **`events`— メディア** トラッキングデータを送信します。

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Request Body {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime`  — すべてのリクエストに対して必須。
* `eventType`  — すべてのリクエストに対して必須。
* `params` - 特定の `eventTypes` に必須です。[JSON 検証スキーマ](mc-api-ref/mc-api-json-validation.md)を調べて、必須の eventTypes とオプションの eventType を確認してください。

* `qoeData`  — すべてのリクエストに対してオプションです。
* `customMetadata`  — すべてのリクエストに対してオプションですが、イベントタイプ、イベ `sessionStart`ントタ `adStart`イプでのみ `chapterStart` 送信されます。

各 `eventType` には公開されている [JSON 検証スキーマ](mc-api-ref/mc-api-json-validation.md)があります。これを使用して、パラメータータイプを確認し、特定のイベントに対してパラメーターがオプションであるか必須であるかを確認してください。

### イベントタイプ {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

