---
title: JSON 検証スキーマ
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# JSON 検証スキーマ{#json-validation-schemas}

Media Analyticsバックエンドは、JSON検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。 これらのスキーマはユーザーが使用でき、MA APIで使用されるパラメータタイプの現在の権限として機能します。

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
