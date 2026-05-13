---
title: テスト 1：標準の再生
description: 検証で使用する標準の再生テストについて説明します。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ChiE4jNDe-8GnbzNp8f9epCCFi6Hq9FkwrLzZEbcxcU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 854
ht-degree: 84%

---

# テスト 1：標準の再生{#test-standard-playback}

このテストケースは、一般的な再生およびシーケンスを検証します。

Media Analytics 実装には、次の 2 つのタイプのトラッキングコールが含まれています。
* Adobe Analytics（AppMeasurement）サーバーに対して直接おこなわれる呼び出し - これらの呼び出しは、「メディア開始」および「広告開始」イベント時に発生します。
* Media Analytics（ハートビート）サーバーに対しておこなわれる呼び出し - これらには、帯域内および帯域外呼び出しが含まれます。
   * 帯域内 - SDK は、時間設定された再生呼び出しまたは「ping」を、コンテンツ再生中は 10 秒間隔、広告中は 1 秒間隔で送信します。
   * 帯域外 - これらの呼び出しは、どの時点でも発生する可能性があり、一時停止、バッファリング、エラー、コンテンツ完了、広告完了などを含む可能性があります。

>[!NOTE]
>メディアトラッキングは、すべてのプラットフォームで同じように動作します。

## テスト手順

次の操作を（順番に）実行して記録します。

1. **ページまたはアプリを読み込む**

   **トラッキングサーバー**（すべての Web サイトおよびモバイルアプリ）：

   * **Adobe Analytics（AppMeasurement）サーバー -** Experience Cloud 訪問者 ID サービスを使用するには、RDC トラッキングサーバー、または RDC サーバーに解決される CNAME が必要です。 Adobe Analytics トラッキングサーバーは「`.sc.omtrdc.net`」で終わるか CNAME である必要があります。

   * **Media Analytics（ハートビート）サーバー -** このサーバーは、常に「`[namespace].hb.omtrdc.net`」形式になります（`[namespace]` は会社名を指定します）。 この名前は、アドビから提供されます。

   すべてのトラッキングコールで共通の、特定のキー変数を検証する必要があります。

   **Adobe 訪問者 ID（`mid`）：** `mid` 変数は、AMCV Cookie に設定される値をキャプチャするために使用されます。 `mid` 変数は、Web サイトとモバイルアプリの両方で識別のための主要な値となると共に、Experience Cloud 訪問者 ID サービスが適切に設定されていることを示します。 Adobe Analytics（AppMeasurement）と Media Analytics（ハートビート）呼び出しの両方で使用されます。

   * **Adobe Analytics Start 呼び出し**

     | パラメーター | 値（サンプル） |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Web サイトページ呼び出し**

     | パラメーター | 値（サンプル） |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **ライフサイクル呼び出し**

     | パラメーター | 値（サンプル） |
     |---|---|
     | `pev2` | ADBINTERNAL:Lifecycle |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics Start 呼び出し**

     | パラメーター | 値（サンプル） |
     |---|---|
     | `s:event:type` | start |

     >[!NOTE]
     >
     >Media Analytics Start 呼び出し（`s:event:type=start`）時に `mid` 値が存在しないことがあります。 これは問題ありません。 Media Analytics Play 呼び出し（`s:event:type=play`）までは表示されないことがあります。

   * **Media Analytics Play 呼び出し**

     | パラメーター | 値（サンプル） |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **メディアプレーヤーを開始する**

   メディアプレーヤーの開始時に、メディア SDK は、次の順序で 2 つのサーバーにキー呼び出しを送信します。

   1. Adobe Analytics サーバー - Start 呼び出し
   1. Media Analytics サーバー - Start 呼び出し
   1. Media Analytics サーバー - 「Adobe Analytics Start call requested」

   上記の最初の 2 つの呼び出しには、追加のメタデータおよび変数が含まれます。 呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#start-the-media-player)を参照してください。

   上記の 3 番目の呼び出しは、Adobe Analytics サーバーに送信される Adobe Analytics Start 呼び出し（`pev2=ms_s`）をメディア SDK がリクエストしたことを Media Analytics サーバーに伝えます。

1. **広告ブレークを視聴する（可能な場合）**

   * **広告開始**

   広告の開始時に、次の順序でキー呼び出しが送信されます。

   1. Adobe Analytics サーバー - Ad Start 呼び出し
   1. Media Analytics サーバー - Ad Start 呼び出し
   1. Media Analytics サーバー - 「Adobe Analytics Ad Start call requested」

   最初の 2 つの呼び出しには、追加のメタデータおよび変数が含まれます。 呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#view-ad-playback)を参照してください。

   3 番目の呼び出しは、Adobe Analytics サーバーに送信される Adobe Analytics Start 呼び出し（`pev2=msa_s`）をメディア SDK がリクエストしたことを Media Analytics サーバーに伝えます。

   * **広告再生**

     広告の再生中、Media Analytics SDK は、1 秒ごとにタイプ「ad」の再生イベントを Media Analytics サーバーに送信します。

   * **広告完了**

     広告の 100％の時点で、Media Analytics Complete 呼び出しが送信される必要があります。

1. **広告再生を 30 秒間一時停止します（可能な場合）。** **広告一時停止**

   広告の一時停止時、1 秒ごとに Media Analytics ハートビートまたは「ping」呼び出しが SDK によって Media Analytics サーバーに送信されます。

   >[!NOTE]
   >
   >一時停止中は、再生ヘッド値が一定である必要があります。

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)を参照してください。

1. **メインコンテンツを中断せずに 10 秒間再生します。** **コンテンツの再生**

   メインコンテンツの再生中、メディア SDK は、10 秒ごとにハートビート（Play 呼び出し）を Media Analytics サーバーに送信します。

   メモ:

   * 再生ヘッドの位置は、1 回の Play 呼び出しにつき 10 秒ずつ増やす必要があります。
   * `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

     呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#play-main-content)を参照してください。

1. **再生中に少なくとも30秒間一時停止します。** Media Playerを一時停止すると、一時停止イベント呼び出しは、SDKによって10秒ごとにMedia Analytics サーバーに送信されます。 一時停止が終わったら、再生イベントを再開する必要があります。

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#pause-main-content)を参照してください。

1. **メディアをシーク/スクラブします。** メディア再生ヘッドのスクラブでは、特別なトラッキング呼び出しは送信されませんが、スクラブ後にメディア再生が再開される場合、再生ヘッドの値はメインコンテンツ内の新しい位置を反映する必要があります。

1. **メディアの再生（VODのみ）。** メディアを再生する際は、新しいMedia Start呼び出しのセットを送信する必要があります（まるで新しい開始であるかのように）。

1. **プレイリスト内の次のメディアを表示します。** プレイリスト内の次のメディアのメディア開始時に、メディア開始呼び出しの新しいセットを送信する必要があります。

1. **メディアまたはストリームを切り替えます。** ライブストリームを切り替える場合、最初のストリームに対するMedia Analyticsの完全な呼び出しを送信しないでください。 メディア開始呼び出しと再生呼び出しは、新しい番組とストリームの名前、新しい番組の適切な再生ヘッドと期間の値を使用して開始される必要があります。
