---
title: ストリーミングメディアコレクション API ‐ イベントリクエストエンドポイント
description: Media Collection API イベントのリクエストエンドポイントパラメーターとレスポンスとは何ですか？
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 76%

---

# Events リクエスト{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI パラメーター

`sid`：[セッションリクエスト](mc-api-sessions-req.md)から返されたセッション ID。

## リクエスト本文

リクエスト本文は、JSON である必要があり、このリクエスト本文の例と同じ構造である必要があります。

```json
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
* `customMetadata`（オプション。`adStart` および `chapterStart` イベントタイプでのみ送信）
* `qoeData` (オプション)

このリリースで有効なイベントタイプの一覧については、[イベントタイプと説明](mc-api-event-types.md)を参照してください。

>[!IMPORTANT]
>
>***広告トラッキング -**`adBreak`* 内の広告のみ追跡できます。
>
>広告の前後に `adBreakStart` と `adBreakComplete` の「ブックエンド」がない場合、`adStart` および `adComplete` イベントは単に無視され、対応する広告期間がメインコンテンツ期間として追跡されます。 これは、Adobe Analytics で使用できる集計データに大きな影響を与える可能性があります。

## 応答

```text
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
| **204** | **コンテンツがありません。** <br/><br/> ハートビート呼び出しが成功しました。 | 該当なし |
| **400** | **リクエストが正しくありません。** <br/><br/> リクエストの形式が正しくありません。 | リクエストタイプについては、[JSON 検証スキーマ](mc-api-json-validation.md)を確認してください。 |
| **404** | **が見つかりません。** <br/><br/> メディアセッションのセッション IDがバックエンドサービスに見つかりませんでした。 | クライアントアプリケーションでは [Sessions リクエスト](mc-api-sessions-req.md) API を使用して、別のメディアセッションおよびそのセッションに対するレポートトラッキングを作成する必要があります。 |
| **410** | **行った。** <br/><br/> メディア セッションがバックエンド サービスで見つかりましたが、クライアントはメディア セッションのアクティビティをレポートできません。 | クライアントアプリケーションでは [Sessions リクエスト](mc-api-sessions-req.md) API を使用して、別のメディアセッションおよびそのセッションに対するレポートトラッキングを作成する必要があります。 |
| **500** | **サーバーエラー** | 該当なし |
