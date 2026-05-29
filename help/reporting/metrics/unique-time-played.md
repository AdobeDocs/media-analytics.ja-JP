---
title: ユニーク再生時間
description: セッション中に個別のコンテンツが表示される秒数をレポートし、シーク・バック・リプレイを重複排除します。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# ユニーク再生時間

**ユニーク再生時間**&#x200B;指標は、セッション中に表示された個別のコンテンツの秒数をレポートし、シーク バックを介して再生されたセグメントを重複排除します。 視聴者が同じセッション内の同じコンテンツの一部を再視聴すると、[ コンテンツに費やした時間](content-time-spent.md)と比較して、一意の再生時間は少なくなります。

## この指標の計算方法

メディアのバックエンドでは、セッション中に再生ヘッドの間隔が表示され、結合が集計されます。 同じ5秒のセグメントを2回プレイしても、5秒としてカウントされます。 この指標は、クローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.uniqueTimePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
