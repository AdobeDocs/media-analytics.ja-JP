---
title: コンテンツセグメントビュー
description: アクティブなメインコンテンツの再生が発生したセグメントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
