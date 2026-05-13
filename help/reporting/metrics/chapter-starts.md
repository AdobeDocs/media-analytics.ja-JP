---
title: 章の開始
description: セッション中に再生を開始したすべての章をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---


# 章の開始

**チャプター開始**&#x200B;指標は、セッション中に再生を開始したすべてのチャプターをカウントします。 [ チャプター完了](chapter-completes.md)と組み合わせて、チャプター完了率を計算します。

## この指標の計算方法

メディア バックエンドは、`media.chapterStart` イベントを受信したときに`mediaReporting.chapterDetails.isStarted = true`を設定します。 この指標は、章のクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
