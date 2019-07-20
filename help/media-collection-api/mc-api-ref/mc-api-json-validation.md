---
seo-title: JSON 検証スキーマ
title: JSON 検証スキーマ
uuid: 7c9d5ce4- f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# JSON 検証スキーマ{#json-validation-schemas}

Media Analyticsのバックエンドは、JSON検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。これらのスキーマはユーザーが使用でき、MA APIで使用されるパラメータータイプの現在の権限として機能します。

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
