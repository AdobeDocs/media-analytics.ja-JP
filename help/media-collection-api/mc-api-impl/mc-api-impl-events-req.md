---
seo-title: Events リクエストの実装
title: Events リクエストの実装
uuid: 3bfa313c- ff74-4e2e- bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Events リクエストの実装{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) 再生ヘッドの場所とタイムスタンプ、イベントタイプおよび含めるオプションのパラメーターを、リクエストのJSON本文に指定します。

[Eventsリクエスト](../../media-collection-api/mc-api-ref/mc-api-events-req.md) のJSONリクエスト本文は、Sessionsリクエストと同じ構造を持っていますが、パラメーター要件およびタイプの [JSON検証スキーマ](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) を確認します。
