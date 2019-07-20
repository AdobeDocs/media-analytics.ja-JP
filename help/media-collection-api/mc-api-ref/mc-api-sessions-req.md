---
seo-title: Sessions リクエスト
title: Sessions リクエスト
uuid: 9609192d-4f7f-4fb5-844f- ea89d47c4e30
translation-type: tm+mt
source-git-commit: f1c9f5f4cbcd4c043e1c7b4a5037c134b2bdd380

---


# Sessions リクエスト{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URIパラメーター

None

## リクエスト本文

リクエスト本文はJSONである必要があり、このサンプルリクエスト本文と同じ構造を持つ必要があります。

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (必須)
   * `playhead` - 秒単位で指定する必要があります。浮動小数点値を使用できます。
   * `ts` - タイムスタンプ。ミリ秒単位で指定する必要があります。
* `eventType` (必須)

   **有効な値:**`sessionStart`
* `params` (必須)
* `customMetadata` (オプション)
* `qoeData` (オプション)

## 応答

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header-部分的 `/api/v1/` にはAPIバージョンを提供します。The part after `[…]sessions/` is the Session ID.

## 応答コード

| HTTP 応答コード | 説明 |
|---|---|
| 201 | セッションが作成されました |
| 400 | 正しくないリクエストです |
| 500 | サーバーエラー |

