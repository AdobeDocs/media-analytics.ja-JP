---
seo-title: 概要
title: 概要
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 概要{#overview}

メディアコレクション API は、クライアント側のメディア SDK の代替として使用できるアドビの RESTful API です。メディアコレクション API を使用すると、プレーヤーで RESTful HTTP 呼び出しを使用してオーディオおよびビデオイベントを追跡できます。メディア収集APIは、Media SDKの同じリアルタイムトラッキングを提供し、さらに1つの追加機能を提供します。

* **ダウンロードされたコンテンツトラッキング**

   この機能を使用すると、ユーザーのデバイスがオンラインに戻るまで、イベントデータをローカルで保存している間、メディアを追跡できます。（詳しくは、[ダウンロードされたコンテンツの追跡](track-downloaded-content.md)を参照してください）。

メディアコレクション API は、基本的に、メディア SDK のサーバー側バージョンとして動作するアダプターです。つまり、メディアSDKドキュメントの一部はメディア収集APIに関連しています。For example, both solutions use the same [Audio and Video Parameters](/help/metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## メディアトラッキングデータのフロー {#section_pwq_n34_qbb}

メディア収集APIを実装するメディアプレイヤーは、RESTful APIトラッキングコールを直接メディアトラッキングコールバックに呼び出しますが、Media SDKを実装するプレーヤーは、プレイヤーアプリケーション内でSDK APIへのトラッキングコールをおこないます。Web 経由で呼び出しを送信する影響の 1 つとして、メディアコレクション API を実装するプレーヤーでは、メディア SDK が自動的に処理する処理の一部を処理する必要があります(Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

メディア収集APIでキャプチャされたトラッキングデータは、メディアSDKプレーヤーでキャプチャされたトラッキングデータとは異なる方法で送信され、最初に処理されますが、バックエンドの同じ処理エンジンが両方のソリューションに使用されます。

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI：**&#x200B;この情報はアドビの担当者から入手します。

**HTTP メソッド：** JSON リクエスト本文を使用した POST。

### API Calls {#mc-api-calls}

* **`sessions`-** サーバーとのセッションを確立し、後続の `events` 呼び出しで使用されるセッションIDを返します。アプリは、トラッキングセッションの開始時にこれを 1 回呼び出します。

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** メディアトラッキングデータを送信します。

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

* `playerTime` - すべてのリクエストに対して必須です。
* `eventType` - すべてのリクエストに対して必須です。
* `params` - 特定の `eventTypes` に必須です。[JSON 検証スキーマ](mc-api-ref/mc-api-json-validation.md)を調べて、必須の eventTypes とオプションの eventType を確認してください。

* `qoeData` - すべてのリクエストのオプションです。
* `customMetadata` - すべてのリクエストのオプションですが、イベントタイプと共 `sessionStart``adStart``chapterStart` に送信されます。

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

