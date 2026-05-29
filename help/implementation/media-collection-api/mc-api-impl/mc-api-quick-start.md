---
title: Streaming Media Collection API - クイックスタート
description: ストリーミングメディア API の基本を学ぶ。 リクエストデータをすばやく確認する方法を説明します。
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/F7NHDQkJVwVc-Th-blxBP8gifT7V55xLqlI1YT-pswc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 294
ht-degree: 82%

---

# クイックスタート{#quick-start}

>[!TIP]
>
>Media Analytics（MA）コレクション API バックエンドサーバーへの [Session リクエスト](../mc-api-ref/mc-api-sessions-req.md)を正常に完了するために必要なリクエストデータを収集します。 （`curl`、Postman などを使用して）リクエストを手動で送信することで、リクエストデータを迅速に確認できます。 これにより、リクエスト内の無効なデータタイプまたは無効な情報に起因する問題があるかどうかに関するフィードバックがすぐに得られます。 [JSON 検証スキーマ](../mc-api-ref/mc-api-json-validation.md)を使用して、適切なリクエストデータを提供していることを確認します。

1. CX Enterprise アプリケーションを実行するために必要な標準のAdobe Analyticsおよび訪問者データを収集します。

   * 訪問者の Experience Cloud 組織 ID
   * 訪問者の Experience Cloud ユーザー ID
   * Analytics レポートスイート ID
   * Analytics トラッキングサーバー URL

1. 呼び出しを成功させるために必要な最小限のデータを含む、`sessions` リクエスト本文の JSON オブジェクトを作成します。 次に例を示します。

   ```json
   {
       "playerTime": {
           "playhead": 0,
           "ts": 1234560890123
       },
       "eventType": "sessionStart",
       "params": {
           "media.playerName": "sample-html5-api-player",
           "analytics.trackingServer": "[YOUR_TS]",
           "analytics.reportSuite": "[YOUR_RSID]",
           "media.contentType": "VOD",
           "media.length": 60.39333333333333,
           "media.id": "MA Collection API Sample Player",
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]",
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe",
           "media.channel": "sample-channel",
           "media.sdkVersion": "va-api-0.0.0",
           "analytics.enableSSL": false
       }
   }
   ```

   >[!NOTE]
   >
   >JSON リクエスト本文内では正しいデータタイプを使用する必要があります。 例：`analytics.enableSSL`にはブール値が必要で、`media.length`には数値などが必要です。[JSON検証スキーマを確認することで、パラメーターの種類と必須と任意の要件を確認できます。](mc-api-validate-reqs.md)

1. Sessions リクエストを MA コレクション API エンドポイントに送信します。 リクエストのペイロードが無効な場合は、問題を特定し、`201 Created` 応答を受け取るまで再試行します。 この `curl` の例では、JSON リクエスト本文は、`sample_data_session` という名前のファイルに格納されています。

   ```sh
   $ curl -i -d \
     @sample_data_session https://{uri}/api/v1/sessions \
     > curl.sessions.out
   
   $ cat curl.sessions.out
   HTTP/1.1 201 Created
   Server: nginx/1.13.5
   Date: Mon, 18 Dec 2017 22:34:12 GMT
   Content-Type: application/octet-stream
   Content-Length: 0
   Connection: keep-alive
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: *
   Access-Control-Allow-Methods: OPTIONS,POST,PUT
   Access-Control-Allow-Headers: Content-Type
   Access-Control-Expose-Headers: Location
   ```

[Sessions リクエスト](../mc-api-ref/mc-api-sessions-req.md)が成功すると、上記のような `201 Created` 応答を受け取ります。 応答の Location ヘッダーにはセッション ID が含まれています。 セッション ID は、後続のすべてのトラッキングコールに必要なので、応答における重要な情報です。 [Sessions リクエスト](../mc-api-ref/mc-api-sessions-req.md)が正常に返されたら、ビデオプレーヤーで MA API を使用してビデオトラッキングの実装を続行できます。
