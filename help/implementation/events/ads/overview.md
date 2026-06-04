---
title: 広告をトラッキング
description: メディア SDK を使用した広告トラッキングの実装の概要です。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# 広告をトラッキング

広告再生の追跡では、広告の改ページ、広告開始、広告完了、広告スキップをカバーしています。 メディアプレーヤーのAPIを使用して、主要なプレイヤーイベントを特定し、必要な広告変数を設定します。

## プレーヤーイベント

| プレイヤーイベント | アクション |
| --- | --- |
| 広告休憩の開始 | AdBreakStartを呼び出してAdBreak オブジェクトを作成 |
| 広告の開始 | 広告オブジェクトを作成し、AdStartを呼び出す |
| 広告が完了 | AdCompleteに電話 |
| 広告スキップ | AdSkipに電話 |
| 広告ブレーク完了 | AdBreakCompleteを呼び出す |

## 実装手順

1. プレロールを含む広告枠の境界が開始されるタイミングを特定し、広告枠オブジェクトを作成します。 フィールド定義については、[Ad break name](/help/implementation/variables/ads/ad-break-name.md)および[Ad break start time](/help/implementation/variables/ads/ad-break-start-time.md)を参照してください。
1. [Ad break start](/help/implementation/events/ads/ad-break-start.md)に電話して、Ad breakのトラッキングを開始します。
1. 広告がいつ開始されるのかを特定し、広告オブジェクトを作成します。 フィールド定義については、[広告名](/help/implementation/variables/ads/ad-name.md)、[広告ID](/help/implementation/variables/ads/ad-id.md)、[広告の長さ](/help/implementation/variables/ads/ad-length.md)、[ ポッドの位置の広告](/help/implementation/variables/ads/ad-in-pod-position.md)、および[広告プレーヤー名](/help/implementation/variables/ads/ad-player-name.md)を参照してください。
1. オプションで、標準の広告メタデータを添付します。 使用可能なキーについては、[広告主](/help/implementation/variables/ads/advertiser.md)、[ キャンペーン ID](/help/implementation/variables/ads/campaign-id.md)、[Creative ID](/help/implementation/variables/ads/creative-id.md)、[Creative URL](/help/implementation/variables/ads/creative-url.md)、[配置ID](/help/implementation/variables/ads/placement-id.md)および[ サイト ID](/help/implementation/variables/ads/site-id.md)を参照してください。
1. [Ad start](/help/implementation/events/ads/ad-start.md)に電話して、広告のトラッキングを開始します。
1. 広告が完了するまで再生されたら、[Ad complete](/help/implementation/events/ads/ad-complete.md)に電話します。
1. 視聴者が広告をスキップした場合は、「広告が完了」ではなく、「[広告スキップ ](/help/implementation/events/ads/ad-skip.md)」と呼び出します。
1. 同じ広告ブレーク内の追加の広告については、手順3 ～ 7を繰り返します。
1. 広告ブレークが完了したら、[広告ブレーク完了](/help/implementation/events/ads/ad-break-complete.md)に電話します。

>[!IMPORTANT]
>
>**プレロール広告：`trackPlay`を`AdBreakStart`および`AdStart`前に呼び出さないでください。** メインコンテンツの最初の`play` pingは[ コンテンツ開始](/help/reporting/metrics/content-starts.md)を増分します。 プレロール広告イベントが発生する前に`trackPlay`が呼び出され、広告中にビューアが脱落した場合、メインコンテンツが再生されなかったとしても、コンテンツ開始は増分されます。 プレロール シナリオの場合、`AdBreakStart`と`AdStart`が送信されるまで`trackPlay`を遅らせます。

>[!NOTE]
>
>広告再生中に報告された再生ヘッドの値は、広告内ではなく、**メインコンテンツ**&#x200B;内の視聴者の位置を表します。 10分間のビデオの前のプレロール広告の場合、広告全体を通して再生ヘッドは`0`です。 5分の時点で開始するミッドロール広告の場合、広告の期間中、再生ヘッドは`300` （秒）のままになります。

## 一般的な問題

### 広告間の予期しないメイン :play呼び出し

連続した広告間で`main:play`件の呼び出しが発生した場合、AdComplete呼び出しと次のAdStart呼び出しの間に250 ミリ秒以上のギャップが存在します。 このギャップが生じると、Media SDKはメインコンテンツのping送信にフォールバックします。これにより、プリロールのシナリオのコンテンツ開始指標を早い段階で設定できます。

**原因：** Media SDKには広告情報が設定されておらず、プレーヤーは再生中であるため、ギャップ時間はメインコンテンツに割り当てられます。

**解決策：**&#x200B;広告が終了したときに直ちに呼び出すのではなく、各広告のAdComplete呼び出しを（最後の広告を除く）遅延させます。 次のように呼び出しをバッチ化します。

* **広告が開始**&#x200B;するたびに：以前の広告が存在し、まだ完了とマークされていない場合は、新しい広告のAdStartを呼び出す&#x200B;*前*&#x200B;にAdCompleteを呼び出します。
* **広告アセットの終了**&#x200B;ごとに、アドコンプリートをすぐに呼び出さないで、延期します。
* **広告ブレークが完了した場合**：最後の広告のAdCompleteを呼び出してから（まだ呼び出されていない場合）、AdBreakCompleteを呼び出します。

このパターンにより、AdCompleteと次のAdStartが連続して実行され、ギャップがなくなります。
