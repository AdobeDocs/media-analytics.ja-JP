---
title: コンテンツ開始
description: メインコンテンツが実際に再生され始めたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 10%

---


# コンテンツ開始

**コンテンツ開始**&#x200B;指標は、メインコンテンツが実際に再生を開始したセッションをカウントします。 [&#x200B; メディア開始](media-starts.md)とは異なり、プレロール広告、バッファリング、またはストール中に終了したセッションは除外されます。 そのため、成約率とエンゲージメント率を適切に区別する必要があります。

## この指標の計算方法

メディアバックエンドは、メインコンテンツの[play](/help/implementation/events/playback/play.md) イベントを初めて受信したときに`mediaReporting.sessionDetails.isPlayed = true`を設定します。 この指標は、その再生イベントでトリガーされますが、クローズコールで報告されます。 プレロールのドロップ率を計算するには、`(Media starts − Content starts) / Media starts`を使用します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.play`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.play` |
