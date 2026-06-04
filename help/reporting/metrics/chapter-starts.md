---
title: 章の開始
description: セッション中に再生を開始したすべての章をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# 章の開始

**チャプター開始**&#x200B;指標は、セッション中に再生を開始したすべてのチャプターをカウントします。 [&#x200B; チャプター完了](chapter-completes.md)と組み合わせて、チャプター完了率を計算します。

## この指標の計算方法

メディアバックエンドは、[章の開始](/help/implementation/events/chapters/chapter-start.md) イベントを受信したときに、このフラグを設定します。 この指標は、章のクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディアチャプター]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.chapter.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
