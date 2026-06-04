---
title: 広告開始
description: セッション中に再生を開始したすべての広告をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

---


# 広告開始

**広告開始**&#x200B;指標は、セッション中に再生を開始したすべての広告をカウントします。 [Ad completes](ad-completes.md)と組み合わせて広告完了率を計算し、同等のセッションレベルのロールアップには[Ad count](/help/reporting/metrics/ad-count.md)を使用します。

## この指標の計算方法

メディア バックエンドは、[広告開始](/help/implementation/events/ads/ad-start.md) イベントを受信したときに、このフラグを設定します。 この指標は、広告開始呼び出しに関して報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.ad.view` |
