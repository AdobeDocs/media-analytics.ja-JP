---
title: カスタムメタデータのサポート
description: sessionStart イベント、chapterStart イベント、adStart イベントでカスタム key:value ペアを指定する方法について説明します。
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# カスタムメタデータのサポート{#custom-metadata-support}

Media Collection APIを使用すると、カスタムキーと値のペアを、`sessionStart`、`adStart`、および`chapterStart` イベントの標準パラメーターと共に送信できます。 カスタムメタデータは、それぞれのメディア終了イベントとともに&#x200B;**Adobe Analytics**&#x200B;に転送されます。

このデータをAnalysis Workspaceで利用できるようにするには、カスタム eVarを定義し、ユースケースに応じて処理ルールを設定する必要があります。 eVarまたはpropにマッピングすると、データは、[Analytics ソースコネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics)が設定されている場合、対応するeVar パスを通じてAdobe Experience Platformでも利用できるようになります。

Experience Edgeを使用するXDM ベースの実装については、[ カスタムメタデータのサポート - XDM フォーマット ](/help/implementation/edge/custom-metadata.md)を参照してください。

## 概要

カスタムメタデータは、リクエスト本文に`customMetadata` オブジェクトとして含まれ、`params` キーと共に配置されます。 これは、次の3つのイベントタイプに適用されます。

| イベント | メタデータの適用先 |
|-------|-------------------|
| `sessionStart` | メインコンテンツ（セッション全体） |
| `adStart` | 個人広告 |
| `chapterStart` | コンテンツの章またはセグメント |

## 構造

カスタムメタデータは、イベントレベルのフラット **オブジェクト** （キーと値のペア）で、`params` キーと一緒に使用します。

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### イベントタイプ別の必須パラメーター

| イベント | 必須`params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### 主要な命名要件

* カスタムメタデータキーで`media.`接頭辞を使用しないでください。標準メディアフィールドにマッピングされ、Analytics レポートで上書きされる可能性があります
* `a.`接頭辞はAdobe標準メタデータ用に予約されているため、使用しないでください

## メインコンテンツのカスタムメタデータ

`sessionStart`様と共に送信されました。 追跡中のプライマリメディアに適用され、広告およびチャプターの呼び出し全体を通じて引き続き利用できます。 ここで定義されたカスタムメタデータは、対応するクローズ呼び出しのメディアバックエンドによって自動的にマージされます。 広告やチャプターに定義された特定のカスタムメタデータと一緒に含まれます。

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## カスタムメタデータの追加

`adStart`様と共に送信されました。 個別の広告に固有のものです。 `sessionStart`のカスタムメタデータも、ここで定義されている広告固有のカスタムメタデータとともに、広告終了呼び出しのメディアバックエンドによって自動的に結合されます。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## 章カスタムメタデータ

`chapterStart`様と共に送信されました。 コンテンツの章やセグメントごとに固有です。 `sessionStart`のカスタムメタデータも、ここで定義されている章固有のカスタムメタデータとともに、章クローズ呼び出しのメディアバックエンドによって自動的に結合されます。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## 動作

* すべてのカスタムメタデータ値は&#x200B;**文字列**&#x200B;である必要があります。 送信前に数値とブール値を変換します。
* カスタムメタデータは、`c.`接頭辞（`contentCategory` → `c.contentCategory`など）を持つAnalyticsに表示されます。
* Analyticsの処理ルールを使用して、カスタムメタデータをeVar、prop、コンテキストデータ変数にマッピングできます
* `sessionStart`個のメタデータはセッション全体で保持されます。更新には新しいセッションが必要です
* 各`adStart`および`chapterStart` イベントには、異なるカスタムメタデータを含めることができます

## 関連ドキュメント

* [ カスタムメタデータのサポート - XDM フォーマット ](/help/implementation/edge/custom-metadata.md) — Experience Edgeを介して、AnalyticsとAEPの両方にカスタムメタデータを送信します
* [ レポートスイートデータ用のAdobe Analytics ソースコネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics) — Analytics データをAdobe Experience Platformに取り込む

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->
