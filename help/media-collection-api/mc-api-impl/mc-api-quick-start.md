---
title: ストリーミングメディアコレクション API - クイックスタート
description: ストリーミングメディア API の基本を学ぶ。 リクエストデータをすばやく確認する方法を説明します。
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# クイックスタート{#quick-start}

>[!TIP]
>
>Media Analytics（MA）コレクション API バックエンドサーバーへの [Session リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を正常に完了するために必要なリクエストデータを収集します。（`curl`、Postman などを使用して）リクエストを手動で送信することで、リクエストデータを迅速に確認できます。これにより、リクエスト内の無効なデータ型または無効な情報に起因する問題があるかどうかに関するフィードバックがすぐに得られます。[JSON 検証スキーマ](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)を使用して、適切なリクエストデータを提供していることを確認します。

1. 標準の必須 Adobe Analytics および訪問者データを収集します。これらは、すべての Experience Cloud アプリケーションを実行するために提供する必要があります。

   * 訪問者の Experience Cloud 組織 ID
   * 訪問者の Experience Cloud ユーザー ID
   * Analytics レポートスイート ID
   * Analytics トラッキングサーバー URL

1. 呼び出しを成功させるために必要な最小限のデータを含む、`sessions` リクエスト本文の JSON オブジェクトを作成します。次に例を示します。

   ```
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
   >JSON リクエスト本文内では正しいデータ型を使用する必要があります。例えば、`analytics.enableSSL` はブール型、`media.length` は数値型です。[JSON 検証スキーマ](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)を調べて、パラメーターのタイプと、それが必須の要件かオプションの要件かを確認できます。

1. Sessions リクエストを MA コレクション API エンドポイントに送信します。リクエストのペイロードが無効な場合は、問題を特定し、`201 Created` 応答を受け取るまで再試行します。この `curl` の例では、JSON リクエスト本文は、`sample_data_session` という名前のファイルに格納されています。

   ```
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

[Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)が成功すると、上記のような `201 Created` 応答を受け取ります。応答の Location ヘッダーにはセッション ID が含まれています。セッション ID は、後続のすべてのトラッキングコールに必要なので、応答における重要な情報です。[Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)が正常に返されたら、ビデオプレーヤーで MA API を使用してビデオトラッキングの実装を続行できます。
