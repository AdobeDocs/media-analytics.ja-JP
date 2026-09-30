---
title: コンテンツセグメントビュー
description: アクティブなメインコンテンツの再生が発生したセグメントをカウントします。
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
source-wordcount: '185'
ht-degree: 9%
---

# コンテンツセグメントビュー

**コンテンツセグメントビュー**&#x200B;指標では、アクティブなメインコンテンツの再生が発生した5分間のコンテンツセグメントがカウントされます。 この指標は、閲覧者が読み込みやバッファリングだけでなく、そのセグメントでコンテンツを再生したことを確認します。 [&#x200B; コンテンツセグメント &#x200B;](/help/reporting/dimensions/content-segment.md) ディメンションと組み合わせて、長文コンテンツビューアのどの部分が実際に消費されたかを分割します。

## この指標の計算方法

メディアバックエンドは、メインコンテンツに対して少なくとも1つの[play](/help/implementation/events/playback/play.md) イベントが受信されたセグメントをカバーするクローズ呼び出しにこのフラグを設定します。 この指標は、クローズ呼び出しで報告されます。 Media Edge API パスでは、セグメントビューはコンテンツの開始と同じ条件で実行されます。 どちらも、メインコンテンツに[play](/help/implementation/events/playback/play.md) イベントが必要です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.segmentView`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
