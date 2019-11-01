---
title: タイムライン 3 - チャプター
description: null
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# タイムライン 3 - チャプター {#timeline-3-chapters}

## VOD、プリロール広告、一時停止、バッファリング、コンテンツの最後まで視聴


次の図は、再生ヘッドのタイムラインと、ユーザーのアクションの対応するタイムラインを示しています。 各アクションの詳細と、それに伴うリクエストを以下に示します。


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## アクションの詳細


### アクション1 — セッションの開始 {#Action-1}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| 自動再生または再生ボタンが押され、ビデオの読み込みが開始される | 0 | 0 | `/api/v1/sessions` |

**実装の詳細**

この呼び出しは、 _ユーザがビデオを再生する意図を_ 、通知します。 It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. プレーヤーの状態はまだ「再生中」ではなく、「開始中」です。[必須のセッションパラメーター](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)をリクエスト本文の `params` マップに含める必要があります。バックエンドでは、この呼び出しによって Adobe Analytics の開始呼び出しが生成されます。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### アクション2 - pingタイマーが開始します {#Action-2}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントタイマーを開始する | 0 | 0 |  |

**実装の詳細**

pingタイマーを起動します。 プリロール広告がある場合は、最初のpingイベントが1秒で起動し、それ以外の場合は10秒です。

### アクション3 — 広告の時間の開始 {#Action-3}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告ブレークの開始を追跡する | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

広告は、広告ブレーク内でのみ追跡できます。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### アクション4 — 広告開始 {#Action-4}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告 #1 の開始を追跡する | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

長さが 15 秒の最初のプリロール広告の追跡を開始します。この `adStart` を使用してカスタムメタデータを含めます。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### アクション5 — 広告のping {#Action-5}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

1秒ごとにバックエンドにpingを実行します。 （以降の広告pingは、簡潔にするために表示されません）。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション6 — 広告完了 {#Action-6}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告 #1 の完了を追跡する | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

最初のプリロール広告の終わりを追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### アクション7 — 広告開始 {#Action-7}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告 #2 の開始を追跡する | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

長さが 7 秒の 2 番目のプリロール広告の開始を追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### アクション8 — 広告のping {#Action-8}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

1秒ごとにバックエンドにpingを実行します。 （以降の広告pingは、簡潔にするために表示されません）。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション9 — 広告完了 {#Action-9}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告 #2 の完了を追跡する | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

2 番目のプリロール広告の終わりを追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### アクション10 — 広告の時間の完了 {#Action-10}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告ブレークの完了を追跡する | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

広告ブレークが終了します。広告ブレーク中、再生状態は「再生中」のままになります。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### アクション11 — コンテンツの再生 {#Action-11}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| 再生イベントを追跡する | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

`adBreakComplete` イベントの後、`play` イベントを使用してプレーヤーを「再生中」状態にします。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### アクション12 — チャプター開始 {#Action-12}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| チャプター開始イベントを追跡する | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

再生イベントの後、最初のチャプターの開始を追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### アクション13 - Ping {#Action-13}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション14 — バッファー開始 {#Action-14}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| バッファー開始イベントが発生した | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

「バッファリング」状態への移行を追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### アクション15 — バッファー終了（再生） {#Action-15}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| バッファリングが終了し、アプリがコンテンツの再開を追跡する | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バッファリングが 3 秒後に終了するので、プレーヤーを「再生中」状態に戻します。バッファリングが終了したら再生イベントの追跡をもう 1 件送信する必要があります。**呼び出`play`しがバックエ`bufferStart`ンドに対して「bufferEnd」呼び出しを送信した後で行われるので** 、イベントは必要ありま `bufferEnd` せん。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### アクション16 - Ping {#Action-16}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション17 — チャプター終了 {#Action-17}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリがチャプターの終わりを追跡する | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

最初のチャプターが 2 番目の広告ブレークの直前に終了します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### アクション18 — 広告の時間の開始 {#Action-18}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告ブレークの開始を追跡する | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

期間が 8 秒のミッドロール広告。`adBreakStart` を送信します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### アクション19 — 広告開始 {#Action-19}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告 #3 の開始を追跡する | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

ミッドロール広告を追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### アクション20 — 広告ping {#Action-20}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

1秒ごとにバックエンドにpingを実行します。 （以降の広告pingは、簡潔にするために表示されません）。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション21 — 広告完了 {#Action-21}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告 #1 の完了を追跡する | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

ミッドロール広告が完了します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### アクション22 — 広告の時間の完了 {#Action-22}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告ブレークの完了を追跡する | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

広告ブレークが完了します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### アクション23 — チャプター開始 {#Action-23}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| チャプター 2 の開始を追跡する | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**



**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### アクション24 - Ping {#Action-24}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション25 — 一時停止 {#Action-25}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ユーザーが一時停止を押した | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

ユーザーアクションによって、再生状態が「一時停止」に移動されます。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### アクション26 - Ping {#Action-26}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。プレーヤーはまだ「バッファリング」状態になっています。ユーザーは、コンテンツの 20 秒時点で停止しています。待ちます...

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション27 — コンテンツの再生 {#Action-27}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ユーザーが再生を押してメインコンテンツを再開する | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

再生状態を「再生中」に移行します。**`play`の後の`pauseStart`呼び出しがバックエンドへの「」呼び出しと解釈される**&#x200B;ので、`resume`resume イベントは必要ありません。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### アクション28 - Ping {#Action-28}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション29 — チャプター終了 {#Action-29}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| チャプター 2 が終了する | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

2 番目と最後のチャプターの終わりを追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### アクション30 — セッション完了 {#Action-30}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ユーザーがコンテンツを最後まで視聴する | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

`sessionComplete` をバックエンドに送信して、ユーザーがコンテンツ全体の視聴を終了したことを示します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**シークイベントがない場合 -** メディアコレクション API では、`seekStart` および `seekComplete` イベントの明示的なサポートはありません。これは、特定のプレーヤーではエンドユーザーがスクラビングすると、これらのイベントが大量に生成され、数百人のユーザーであってもバックエンドサービスのネットワーク帯域幅のボトルネックになり得るからです。アドビでは、再生ヘッドの位置ではなく、デバイスのタイムスタンプに基づいてハートビート期間を計算することで、シークイベントの明示的なサポートの代わりとしています。

