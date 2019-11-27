---
title: Events リクエストの実装
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Events リクエストの実装 {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Sessions リクエストを使用してセッション ID を取得した後、後続のすべてのトラッキングコールに対して [Events リクエスト](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)を使用します（Sessions リクエストについては、[こちらを参照）。](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) リクエストの JSON 本文に、再生ヘッドの位置、タイムスタンプ、イベントタイプおよび含めたい任意のオプションパラメーターを指定します。

[Events リクエスト](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)の JSON リクエスト本文は、Sessions リクエストと同じ構造です。ただし、パラメーターの要件およびタイプについては、[JSON 検証スキーマ](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)を確認してください。
