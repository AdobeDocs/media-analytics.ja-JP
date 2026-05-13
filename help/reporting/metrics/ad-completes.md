---
title: 広告完了
description: 完了まで再生したすべての広告をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# 広告完了

**Ad completes**&#x200B;指標は、完了まで再生したすべての広告をカウントします。 [広告が](ad-starts.md)を開始して広告の完了率を計算します。

## この指標の計算方法

メディア バックエンドは、`media.adComplete` イベントを受信したときに`mediaReporting.advertisingDetails.isCompleted = true`を設定します。 この指標は、広告クローズ呼び出しに関してレポートされます。 スキップまたは放棄された広告は、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
