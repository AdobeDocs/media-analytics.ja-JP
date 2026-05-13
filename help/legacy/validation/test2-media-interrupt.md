---
title: テスト 2 メディアの中断
description: 検証で使用するメディア中断テストについて説明します。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# テスト 2：メディアの中断{#test-media-interruption}

このテストケースは、モバイルの中断動作を検証します。

## テスト手順

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレーヤーを開始する**

   メディアプレーヤーの開始時に、次の順序で呼び出しが送信されます。

   1. Adobe Analytics（AppMeasurement）Start
   1. Media Analytics（ハートビート）Start
   1. Media Analytics（ハートビート）Adobe Analytics Start 呼び出しがリクエストされる

   上記の最初の 2 つの呼び出しには、追加のメタデータおよび変数が含まれます。 呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#start-the-media-player)を参照してください。

   上記の 3 番目の呼び出しは、Adobe Analytics サーバーに送信される Adobe Analytics Start 呼び出し（`pev2=ms_s`）をメディア SDK がリクエストしたことを Media Analytics サーバーに伝えます。

1. **メインコンテンツを中断せずに 5 分以上間再生する**

   **コンテンツの再生**

   コンテンツの再生中、メディア SDK は、10 秒ごとに再生呼び出し（ハートビート）を Media Analytics サーバーに送信します。

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#play-main-content)を参照してください。

   また、これらの広告呼び出しの追加情報については、お使いのプラットフォームの[広告の追跡](/help/use-cases/track-ads/track-ads-overview.md)の手順も参照してください。

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   アプリがバックグラウンドで実行されている間、`main:pause` 呼び出しのみが Media Analytics サーバーに送信される必要があります（VHL バージョン 1.6.6 以降）。

1. **アプリまたはブラウザーをフォアグラウンドに移動する**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **メインコンテンツメディアを中断せずに 5 分以上間再生する**

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#play-main-content)を参照してください。

1. **メディアプレーヤーを閉じる**

   メディアプレーヤーが閉じられた後は、追加のトラッキングコールを発生させないでください。
