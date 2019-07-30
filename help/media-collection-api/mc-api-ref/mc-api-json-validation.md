---
seo-title: JSON 検証スキーマ
title: JSON 検証スキーマ
uuid: 7c9d5ce4- f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JSON 検証スキーマ{#json-validation-schemas}

Media Analyticsのバックエンドは、JSON検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。これらのスキーマはユーザーが使用でき、MA APIで使用されるパラメータータイプの現在の権限として機能します。

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
