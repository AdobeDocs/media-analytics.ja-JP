---
title: メディア滞在時間
description: 広告を含む、セッションごとのアクティブな再生の合計秒数をレポートします。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 8%
---

# メディア滞在時間

**メディア滞在時間**&#x200B;指標は、セッションごとのアクティブな再生の合計秒数をレポートします。これには、メインコンテンツと広告の両方が含まれますが、一時停止、バッファリング、ストールは含まれません。 視聴者がプレーヤーと積極的にエンゲージした合計時間を測定するために使用します。 メインコンテンツの場合のみ、[&#x200B; コンテンツ滞在時間](content-time-spent.md)を使用します。

## この指標の計算方法

メディアバックエンドは、メインコンテンツまたは広告で、プレーヤーが`play`状態にある間に、イベント間の経過時間を合計します。 一時停止、バッファーイベント、ストール中の時間は除外されます。 この指標は、クローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.totalTimePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
