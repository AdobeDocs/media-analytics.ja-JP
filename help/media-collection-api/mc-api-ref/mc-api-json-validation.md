---
title: ストリーミングメディア分析JSON検証スキーマ
description: Steaming Media JSON検証スキーマとは何ですか。また、スキーマを使用して、各タイプのイベントに対する正しいリクエスト本文のパラメーターを判断する方法も示します。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 64%

---

# JSON 検証スキーマ{#json-validation-schemas}

Media Analytics バックエンドは、JSON 検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。これらのスキーマは、ユーザーが利用でき、MA API で使用されているパラメータータイプに関する現在の典拠として機能します。

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

JSON 検証スキーマの使用方法について詳しくは、[イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)を参照してください。
