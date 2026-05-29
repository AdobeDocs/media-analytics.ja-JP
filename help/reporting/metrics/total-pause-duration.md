---
title: 合計一時停止時間
description: 視聴者がセッション中に一時停止した累積秒数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# 合計一時停止時間

**合計一時停止の時間**&#x200B;指標は、視聴者がセッション中に一時停止した累積秒数を報告します。 この指標は、各[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントとその後の[再生](/help/implementation/events/playback/play.md) イベントの間のすべての間隔の合計です。 複数の一時停止が一緒に追加されます。 [一時停止イベント &#x200B;](pause-events.md)と組み合わせて、平均一時停止の長さを求めます。

## この指標の計算方法

メディアバックエンドは、[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントと一致する[再生](/help/implementation/events/playback/play.md) イベントの間の経過時間を合計します。 この指標は、クローズ呼び出しで報告されます。 この値は、Analysis Workspaceでは`HH:MM:SS`として表示され、他の場所では秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.pauseTime`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
