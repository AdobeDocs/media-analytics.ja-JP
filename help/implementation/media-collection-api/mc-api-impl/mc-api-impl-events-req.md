---
title: Events リクエストの実装
description: セッション ID を取得した後、後続のすべてのトラッキングコールで Events リクエストエンドポイントを使用する方法を説明します
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%

---

# Events リクエストの実装 {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Sessions リクエストを使用してセッション ID を取得した後、後続のすべてのトラッキングコールに対して [Events リクエスト](../mc-api-ref/mc-api-events-req.md)を使用します（Sessions リクエストについては、[こちらを参照）。](../mc-api-ref/mc-api-sessions-req.md) リクエストの JSON 本文に、再生ヘッドの位置、タイムスタンプ、イベントタイプおよび含めたい任意のオプションパラメーターを指定します。

[Events リクエスト](../mc-api-ref/mc-api-events-req.md)の JSON リクエスト本文は、Sessions リクエストと同じ構造です。ただし、パラメーターの要件およびタイプについては、[JSON 検証スキーマ](../mc-api-ref/mc-api-json-validation.md)を確認してください。
