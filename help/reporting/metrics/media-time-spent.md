---
title: メディア滞在時間
description: 広告を含む、セッションごとのアクティブな再生の合計秒数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 7%

---


# メディア滞在時間

**メディア滞在時間**&#x200B;指標は、セッションごとのアクティブな再生の合計秒数をレポートします。これには、メインコンテンツと広告の両方が含まれますが、一時停止、バッファリング、ストールは含まれません。 視聴者がプレーヤーと積極的にエンゲージした合計時間を測定するために使用します。 メインコンテンツの場合のみ、[ コンテンツ滞在時間](content-time-spent.md)を使用します。

## この指標の計算方法

メディアバックエンドは、メインコンテンツまたは広告で、プレーヤーが`play`状態にある間に、イベント間の経過時間を合計します。 一時停止、バッファーイベント、ストール中の時間は除外されます。 この指標は、クローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.totalTimePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
