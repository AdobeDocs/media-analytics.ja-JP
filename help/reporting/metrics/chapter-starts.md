---
title: 章の開始
description: セッション中に再生を開始したすべての章をカウントします。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
