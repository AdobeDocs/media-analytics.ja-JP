---
title: 章完了
description: 完了まで再生したすべての章をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 12%

---


# 章完了

**章が完了しました**&#x200B;指標では、完了まで再生したすべての章がカウントされます。 [&#x200B; チャプター開始](chapter-starts.md)と組み合わせて、チャプター完了率を計算します。

## この指標の計算方法

メディア バックエンドは、[章の完了](/help/implementation/events/chapters/chapter-complete.md) イベントを受信したときに`mediaReporting.chapterDetails.isCompleted = true`を設定します。 この指標は、章のクローズ呼び出しで報告されます。 再生中にスキップまたは放棄された章は、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
