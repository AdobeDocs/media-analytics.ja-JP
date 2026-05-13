---
seo-title: Overview
title: ストリーミングメディアコレクション API の概要
description: Media Collection API について説明し、RESTful HTTP 呼び出しを使用してオーディオおよびビデオイベントをプレーヤーでトラッキングする方法について説明します。
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 96%

---

# メディアコレクション API の概要 {#overview}

メディアコレクション API は、クライアント側のメディア SDK の代替として使用できるアドビの RESTful API です。 メディアコレクション API を使用すると、プレーヤーで RESTful HTTP 呼び出しを使用してオーディオおよびビデオイベントを追跡できます。

メディアコレクション API は、基本的に、メディア SDK のサーバーサイドバージョンとして動作するアダプターです。 ストリーミングメディア追跡データを収集すると、同じ[ レポートと分析](/help/reporting/media-reports-enable.md)につながります。

## メディアトラッキングデータのフロー {#media-tracking-data-flows}

メディアコレクション API を実装するメディアプレーヤーは、メディアバックエンドサーバーに対して RESTful API トラッキングコールを直接送信します。一方、メディア SDK を実装するプレーヤーは、プレーヤーアプリ内で SDK API に対してトラッキングコールを送信します。 Web 経由で呼び出しを送信する影響の 1 つとして、メディアコレクション API を実装するプレーヤーでは、メディア SDK が自動的に処理する処理の一部を処理する必要があります （詳しくは、[メディアコレクション実装](mc-api-impl/mc-api-quick-start.md)を参照）。

メディアコレクション API でキャプチャされたトラッキングデータは、送信された後、最初はメディア SDK プレーヤーでキャプチャされたトラッキングデータと異なる方法で処理されます。ただし、どちらもバックエンドの同じ処理エンジンが使用されます。

![](assets/col_api_overview_simple.png)

## API の概要 {#api-overview}

**URI：**&#x200B;この情報はアドビの担当者から入手します。

**HTTP メソッド：** JSON リクエスト本文を使用した POST。

### API 呼び出し {#mc-api-calls}

* **`sessions`-** サーバーとのセッションを確立し、後続の `events` 呼び出しで使用するセッション ID を返します。 アプリは、トラッキングセッションの開始時にこれを 1 回呼び出します。

  `{uri}/api/v1/sessions`

* **`events`-** メディアトラッキングデータを送信します。

  `{uri}/api/v1/sessions/{session-id}/events`

### リクエスト本文 {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - すべてのリクエストに必須です。
* `eventType` - すべてのリクエストに必須です。
* `params` - 特定の `eventTypes` に必須です。[JSON 検証スキーマ](mc-api-ref/mc-api-json-validation.md)を調べて、必須の eventTypes とオプションの eventType を確認してください。

* `qoeData` - すべてのリクエストでオプションです。
* `customMetadata` - すべてのリクエストでオプションです。ただし、`sessionStart`、`adStart` および `chapterStart` イベントタイプでのみ送信されます。

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
* `stateStart`
* `stateEnd`
