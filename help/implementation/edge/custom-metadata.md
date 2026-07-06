---
title: カスタムメタデータのサポート - XDM形式
description: Experience Edge XDM フォーマットを使用して、メディアトラッキングイベントでカスタムメタデータを送信する方法を説明します。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 2%

---


# カスタムメタデータのサポート - XDM形式

Experience Edge APIを使用すると、`sessionStart`、`adStart`、および`chapterStart` API イベントの標準XDM フィールドと一緒にメディアカスタムメタデータを送信できます。 XDM フォーマットを介して送信されたメディアカスタムメタデータは、**Adobe Analytics**&#x200B;と&#x200B;**Adobe Experience Platform**&#x200B;の両方に転送できます。

Media Collection API実装については、[&#x200B; カスタムメタデータのサポート &#x200B;](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)を参照してください。

## 概要

Adobe Experience Edgeリクエスト内の2つの場所に、それぞれ異なるルーティング動作でメディアカスタムメタデータを送信できます。

| 場所 | Adobe Analyticsに送信 | Adobe Experience Platformに送信 | 使用例 |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅はい | ✅はい | 両方のシステムで必要なビジネスデータ |
| `_data` | ✅はい | ❌いいえ | Analytics固有のフラグまたは処理ヒント |

カスタムメタデータは、次の3つのイベントタイプに適用されます。

| イベント | メタデータの適用先 |
|-------|-------------------|
| `sessionStart` | メインコンテンツ（セッション全体） |
| `adStart` | 個人広告 |
| `chapterStart` | コンテンツの章またはセグメント |

## 構造

### `xdm.mediaCollection.customMetadata` （Analytics + AEP）

カスタムメタデータは、`mediaCollection` オブジェクト内の&#x200B;**名前値オブジェクトの配列**&#x200B;です。

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

<InlineAlert variant="warning" slots="text" />

`customMetadata`は、`xdm` ルートレベルではなく、`mediaCollection`内の&#x200B;**配列**&#x200B;である必要があります。

**正しくない：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**正解：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` （Analyticsのみ）

`_data` オブジェクトは、AEP データセットをバイパスして、Adobe Analyticsにのみデータを送信する特別なExperience Edge構造です。 カスタムメタデータは`__adobe.analytics.contextData`の下に配置する必要があります。

名前値オブジェクト **の**&#x200B;配列を使用する`xdm.mediaCollection.customMetadata`とは異なり、`_data` マッピングでは、`contextData`の直下にフラット **キー値オブジェクト**&#x200B;を使用します。

| アプローチ | 構造 | 宛先 |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | `{"name": "...", "value": "..."}` オブジェクトの配列 | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | フラット キー値オブジェクト `{"key": "value"}` | Analyticsのみ |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### 命名規則

* **XDM形式：**&#x200B;接頭辞と、アンダースコアを使用したテナント名前空間。 テナントカスタムフィールドグループ（`_<tenant>.<struct_name>.<field_name>`など）に構造を作成することもできます。
* **`_data`形式：** フィールドが`_data.__adobe.analytics.contextData`の下に配置されます。 フィールド名にアンダースコアのプレフィックスは必要ありません（例：`debugFlag`）。

## メインコンテンツのカスタムメタデータ

`sessionStart`様と共に送信されました。 追跡中のプライマリメディアに適用され、広告およびチャプターの呼び出し全体を通じて引き続き利用できます。 ここで定義されたカスタムメタデータは、対応するクローズ呼び出しのメディアバックエンドによって自動的にマージされます。 広告やチャプターに定義された特定のカスタムメタデータと一緒に含まれます。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### リクエスト

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## カスタムメタデータの追加

`adStart`様と共に送信されました。 個別の広告に固有のものです。 `sessionStart`のカスタムメタデータも、ここで定義されている広告固有のカスタムメタデータとともに、広告終了呼び出しのメディアバックエンドによって自動的に結合されます。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### リクエスト

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## 章カスタムメタデータ

`chapterStart`様と共に送信されました。 コンテンツの章やセグメントごとに固有です。 `sessionStart`のカスタムメタデータも、ここで定義されている章固有のカスタムメタデータとともに、章クローズ呼び出しのメディアバックエンドによって自動的に結合されます。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### リクエスト

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## `_data` オブジェクトの使用（Analytics専用メタデータ）

**not**&#x200B;がAEP データセットに保存されるAdobe Analyticsのメタデータが必要な場合は、`_data` オブジェクトを使用します。 例としては、一時フラグ、デバッグ変数、Analytics固有の処理ヒントなどがあります。

<InlineAlert variant="warning" slots="text" />

`_data`を介して送信されたデータはAdobe Experience Platformに保存されないため、Real-Time CDP、Journey Orchestration、またはその他のAEP サービスでは使用できません。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### リクエスト

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

この例では、次のようになります。

* `_mycompany.league`→AnalyticsとAEPの両方に送信されました
* `debugMode`と`testFlag` （`_data.__adobe.analytics.contextData`未満）→Analyticsにのみ送信されます


## 下流のデータの場所

<InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata`は、イベントを含むカスタムメタデータの送信に使用される&#x200B;**受信API パス**&#x200B;です。 処理後、データはコンテキストデータ変数としてAdobe Analyticsに転送され、`xdm.mediaReporting.customMetadata`の下のAdobe Experience Platformと最上位の統合フィールドとして保存されます。

**Adobe Analytics：**

* 処理後、カスタムメタデータはコンテキストデータ変数としてAdobe Analyticsに転送されます。 `_tenant`接頭辞は自動的に削除されるので、処理ルールは`_tenant`の後のフィールドパスのみを参照します（例：`_mycompany.contentCategory`は`contentCategory`になります）。
* `_data`を介して送信されたデータもAdobe Analyticsに転送され、処理ルールを介して利用できます
* 処理ルールを使用して、コンテキストデータ変数をeVar、prop、またはその他のAnalytics変数にマッピングします。 詳しくは、[Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/ja/docs/analytics/implementation/aep-edge/data-var-mapping)のデータ変数マッピングを参照してください。

**Adobe Experience Platform:**

* カスタムメタデータフィールドは、XDM スキーマのカスタムフィールド（`_mycompany`など）として定義する必要があり、AEPでフラット化されたフィールドとして保存してクエリできます

  ![XDM スキーマのカスタムフィールド定義](assets/custom_metadata.png)
* レポートとクエリの場合、カスタムメタデータは`xdm.mediaReporting.customMetadata`の下および最上位の統合フィールドとしても使用できます。 ユースケースに最も適したツールを選択します。
* セグメンテーション、Journey Orchestration、Real-Time CDPのアクティベーションにアクセス可能

## 動作

* すべてのカスタムメタデータ値は&#x200B;**文字列**&#x200B;である必要があります。 送信前に数値とブール値を変換します。
* `sessionStart`個のメタデータはセッション全体で保持されます。更新には新しいセッションが必要です
* 各`adStart`および`chapterStart` イベントには、異なるカスタムメタデータを含めることができます
* 標準フィールドが存在する場合は、カスタムメタデータよりも標準XDM フィールド （`sessionDetails`、`advertisingDetails`、`chapterDetails`）を優先する

>[!MORELIKETHIS]
>
>* [Media Collection API カスタムメタデータのサポート &#x200B;](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
>* [&#x200B; メディアコレクションの詳細データタイプ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-collection-details)
>* [Adobe Experience Platform Edge Networkのデータ変数マッピング &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/implementation/aep-edge/data-var-mapping)
