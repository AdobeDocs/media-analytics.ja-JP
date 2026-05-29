---
title: 章完了
description: 完了まで再生したすべての章をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# 章完了

**章が完了しました**&#x200B;指標では、完了まで再生したすべての章がカウントされます。 [ チャプター開始](chapter-starts.md)と組み合わせて、チャプター完了率を計算します。

## この指標の計算方法

メディアバックエンドは、[章が完了した](/help/implementation/events/chapters/chapter-complete.md) イベントを受信したときに、このフラグを設定します。 この指標は、章のクローズ呼び出しで報告されます。 再生中にスキップまたは放棄された章は、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
