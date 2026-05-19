---
title: Events リクエストの実装
description: セッション ID を取得した後、後続のすべてのトラッキングコールで Events リクエストエンドポイントを使用する方法を説明します
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# Events リクエストの実装{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

[&#x200B; セッション要求](../mc-api-ref/mc-api-sessions-req.md)を使用してセッション IDを取得した後、後続のすべてのトラッキング呼び出しには、[&#x200B; イベント要求](../mc-api-ref/mc-api-events-req.md)を使用します。 再生ヘッドの場所とタイムスタンプ、イベントタイプ、および含める任意のオプションのパラメーターをリクエストのJSON本文に指定します。

[Events リクエスト](../mc-api-ref/mc-api-events-req.md)の JSON リクエスト本文は、Sessions リクエストと同じ構造です。ただし、パラメーターの要件およびタイプについては、[JSON 検証スキーマ](../mc-api-ref/mc-api-json-validation.md)を確認してください。
