---
title: コンテンツ開始
description: メインコンテンツが実際に再生され始めたセッションをカウントします。
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
source-wordcount: '148'
ht-degree: 10%
---

# コンテンツ開始

**コンテンツ開始**&#x200B;指標は、メインコンテンツが実際に再生を開始したセッションをカウントします。 [ メディア開始](media-starts.md)とは異なり、プレロール広告、バッファリング、またはストール中に終了したセッションは除外されます。 そのため、成約率とエンゲージメント率を適切に区別する必要があります。

## この指標の計算方法

メディアバックエンドは、メインコンテンツの[play](/help/implementation/events/playback/play.md) イベントを初めて受信したときに、このフラグを設定します。 この指標は、その再生イベントでトリガーされますが、クローズコールで報告されます。 プレロールのドロップ率を計算するには、`(Media starts − Content starts) / Media starts`を使用します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.play`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.play` |
