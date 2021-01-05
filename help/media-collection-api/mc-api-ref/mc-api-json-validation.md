---
title: JSON 検証スキーマ
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: ht
source-git-commit: 9b2f8b14ddb5b814f57c752665b78409e31173e8
workflow-type: ht
source-wordcount: '55'
ht-degree: 100%

---


# JSON 検証スキーマ {#json-validation-schemas}

Media Analytics バックエンドは、JSON 検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。これらのスキーマは、ユーザーが利用でき、MA API で使用されているパラメータータイプに関する現在の典拠として機能します。

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

JSON 検証スキーマの使用方法について詳しくは、[イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)を参照してください。
