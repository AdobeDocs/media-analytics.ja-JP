---
title: コンテンツ滞在時間
description: セッションごとのアクティブなメインコンテンツ再生の合計秒数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 7%

---


# コンテンツ滞在時間

**コンテンツ滞在時間**&#x200B;指標は、広告、一時停止、バッファリング、ストールを除いた、セッションごとのアクティブなメインコンテンツの再生合計秒数を報告します。 コンテンツ表示のエンゲージメント指標として使用します。広告を含む滞在時間については、[&#x200B; メディア滞在時間](media-time-spent.md)を参照してください。

## この指標の計算方法

メディアバックエンドは、プレーヤーがメインコンテンツの`play`状態にある間に、イベント間の経過時間を合計します。 広告、一時停止、バッファーイベント、ストール中の時間は除外されます。 この指標は、クローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.timePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
