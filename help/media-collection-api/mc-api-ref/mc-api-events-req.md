---
seo-title: Events リクエスト
title: Events リクエスト
uuid: b237f0a0- dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Events リクエスト{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URIパラメーター

`sid`: [Sessionsリクエストから返されたセッションID。](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## リクエスト本文

リクエスト本文はJSONである必要があり、このサンプルリクエスト本文と同じ構造を持つ必要があります。

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (必須)
   * `playhead` - 秒単位で指定する必要があります。浮動小数点値を使用できます。
   * `ts` - タイムスタンプ。ミリ秒単位で指定する必要があります。
* `eventType` (必須)
* `params` (オプション)
* `customMetadata` （オプション;イベントタイプと共 `adStart``chapterStart` にのみ送信）
* `qoeData` (オプション)

For a list of valid event types for this release, see [Event types and descriptions.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***広告トラッキング-**広告内の広告のみ追跡`adBreak`*&#x200B;できます。
>
>広告の前後に `adBreakStart` と `adBreakComplete` の「ブックエンド」がない場合、`adStart` および `adComplete` イベントは単に無視され、対応する広告期間がメインコンテンツ期間として追跡されます。これは、Adobe Analytics で使用できる集計データに大きな影響を与える可能性があります。

## 応答

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP 応答コード

| HTTP 応答コード | 説明 | クライアントのアクション項目 |
|---|---|---|
| **204** | **No Content.**<br/><br/> ハートビート呼び出しが成功しました。 | 該当なし |
| **400** | **Bad Request.**<br/><br/> リクエストの形式が正しくありません。 | リクエストタイプについては、[JSON 検証スキーマ](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)を確認してください。 |
| **404** | **Not Found.**<br/><br/>メディアセッションのセッションIDがバックエンドサービスで見つかりませんでした。 | クライアントアプリケーションでは [Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API を使用して、別のメディアセッションおよびそのセッションに対するレポートトラッキングを作成する必要があります。 |
| **410** | **Gone.**<br/><br/>メディアセッションがバックエンドサービスで見つかりましたが、クライアントはアクティビティをレポートできません。 | クライアントアプリケーションでは [Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API を使用して、別のメディアセッションおよびそのセッションに対するレポートトラッキングを作成する必要があります。 |
| **500** | **サーバーエラー** | 該当なし |

