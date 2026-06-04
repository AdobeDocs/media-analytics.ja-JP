---
title: 広告完了
description: 完了まで再生したすべての広告をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# 広告完了

**Ad completes**&#x200B;指標は、完了まで再生したすべての広告をカウントします。 [広告が](ad-starts.md)を開始して広告の完了率を計算します。

## この指標の計算方法

メディア バックエンドは、[広告が完了した](/help/implementation/events/ads/ad-complete.md) イベントを受信したときに、このフラグを設定します。 この指標は、広告クローズ呼び出しに関してレポートされます。 スキップまたは放棄された広告は、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
