---
seo-title: タイムライン 2 - ユーザーが中断したセッション
title: タイムライン 2 - ユーザーが中断したセッション
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# タイムライン 2 - ユーザーが中断したセッション {#timeline--2-user-abandons-session}

## VOD、プリロール広告、ミッドロール広告、ユーザーがコンテンツを早い時点で中断

次の図は、再生ヘッドのタイムラインと、ユーザーのアクションの対応するタイムラインを示しています。 各アクションの詳細と、それに伴うリクエストを以下に示します。


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## アクションの詳細

### アクション1 — セッションの開始 {#Action-1}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| 自動再生または再生ボタンが押された | 0 | 0 | `/api/v1/sessions` |

**実装の詳細**

この呼び出しは、ビデオを&#x200B;_再生しようとするユーザーの意図_&#x200B;を示します。It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. プレーヤーの状態はまだ「再生中」ではなく、「開始中」です。[必須のセッションパラメーター](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)をリクエスト本文の `params` マップに含める必要があります。バックエンドでは、この呼び出しによって Adobe Analytics の開始呼び出しが生成されます。

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
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### アクション2 - pingタイマーの開始 {#Action-2}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントタイマーを開始する | 0 | 0 |  |

**実装の詳細**

アプリのpingタイマーを開始します。 プリロール広告がある場合は、最初のpingイベントが1秒で起動し、それ以外の場合は10秒です。

### アクション3 — 広告の時間の開始 {#Action-3}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告ブレークの開始を追跡する | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

プリロール広告を追跡する必要があります。広告は、広告ブレーク内でのみ追跡できます。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### アクション4 — 広告開始 {#Action-4}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告 #1 の開始を追跡する | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

12 秒の広告が開始されます。

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
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### アクション5 — 広告のping {#Action-5}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

1秒ごとにバックエンドにpingを実行します。 （後続の広告pingは、簡潔にするために表示されません）。

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
| プリロール広告 #1 の完了を追跡する | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

最初のプリロール広告が終了します。

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

### アクション7 — 広告の時間の完了 {#Action-7}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| プリロール広告ブレークの完了を追跡する | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

広告ブレークが終了します。広告ブレーク中、プレーヤーの状態は「再生中」のままになります。

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

### アクション8 — コンテンツの再生 {#Action-8}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| 再生イベントを追跡する | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

プレーヤーを「再生中」状態に移行します。コンテンツ再生の開始の追跡を開始します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### アクション9 - Ping {#Action-9}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション10 - Ping {#Action-10}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション11 — エラー {#Action-11}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| エラーが発生し、アプリがエラー情報を送信する | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**


**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### アクション12 — コンテンツの再生 {#Action-12}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリがエラーから回復し、ユーザーが再生を押す | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**



**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### アクション13 - Ping {#Action-13}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| アプリが ping イベントを送信する | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

バックエンドに対する ping を 10 秒ごとに実行します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### アクション14 — 広告の時間の開始 {#Action-14}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告ブレークの開始を追跡する | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

期間が 8 秒のミッドロール広告。`adBreakStart` を送信します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### アクション15 — 広告開始 {#Action-15}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ミッドロール広告 #1 の開始を追跡する | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

ミッドロール広告を追跡します。

**サンプルリクエスト本文**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### アクション16 — アプリを閉じる {#Action-16}

| アクション | アクションタイムライン（秒） | 再生ヘッドの位置（秒） | クライアントリクエスト |
| --- | :---: | :---: | --- |
| ユーザーがアプリを閉じ、視聴を中断したユーザーがこのセッションに戻らないとアプリが判断する | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**実装の詳細**

`sessionEnd` を VA バックエンドに送信して、それ以上の処理をおこなうことなくセッションを即座に終了する必要があることを示します。

**サンプルリクエスト本文**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```


