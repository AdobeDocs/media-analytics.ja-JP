---
title: イベントを一時停止
description: セッション中に発生したすべての個別の一時停止をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 10%

---


# イベントを一時停止

**一時停止イベント**&#x200B;指標は、同じセッション内の複数の一時停止を含め、セッション中に受信した個別の`media.pauseStart` イベントをすべてカウントします。 [合計一時停止デュレーション &#x200B;](total-pause-duration.md)と組み合わせて平均一時停止の長さを導き出し、[影響を受けるストリーム &#x200B;](paused-impacted-streams.md)と組み合わせて、少なくとも1回一時停止したセッションをカウントします。

## この指標の計算方法

メディア バックエンドは、`media.pauseStart`個のイベントごとに`mediaReporting.sessionDetails.pauseCount`増加します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.pauseCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
