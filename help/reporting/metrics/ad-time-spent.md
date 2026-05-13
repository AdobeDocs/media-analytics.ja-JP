---
title: 広告滞在時間
description: セッションあたりのアクティブな広告再生の合計秒数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---


# 広告滞在時間

**広告滞在時間**&#x200B;指標は、一時停止、バッファリング、ストールを除いた、セッションごとのアクティブな広告再生の合計秒数を報告します。 [ コンテンツに費やした時間](/help/reporting/metrics/content-time-spent.md)と組み合わせて、広告の読み込みをコンテンツエンゲージメントと比較します。

## この指標の計算方法

メディアバックエンドは、プレーヤーが広告の`play`状態にある間に、イベント間の経過時間を合計します。 一時停止およびバッファリング中の時間は除外されます。 この指標は、広告クローズ呼び出しに関してレポートされます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.timePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
