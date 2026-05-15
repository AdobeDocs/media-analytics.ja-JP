---
title: 章の開始
description: セッション中に再生を開始したすべての章をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 13%

---


# 章の開始

**チャプター開始**&#x200B;指標は、セッション中に再生を開始したすべてのチャプターをカウントします。 [ チャプター完了](chapter-completes.md)と組み合わせて、チャプター完了率を計算します。

## この指標の計算方法

メディア バックエンドは、[章の開始](/help/implementation/events/chapters/chapter-start.md) イベントを受信したときに`mediaReporting.chapterDetails.isStarted = true`を設定します。 この指標は、章のクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
