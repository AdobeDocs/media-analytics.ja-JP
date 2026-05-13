---
title: コンテンツセグメントビュー
description: アクティブなメインコンテンツの再生が発生したセグメントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# コンテンツセグメントビュー

**コンテンツセグメントビュー**&#x200B;指標では、アクティブなメインコンテンツの再生が発生した5分間のコンテンツセグメントがカウントされます。 この指標は、閲覧者が読み込みやバッファリングだけでなく、そのセグメントでコンテンツを再生したことを確認します。 [&#x200B; コンテンツセグメント &#x200B;](/help/reporting/dimensions/content-segment.md) ディメンションと組み合わせて、長文コンテンツビューアのどの部分が実際に消費されたかを分割します。

## この指標の計算方法

メディアバックエンドは、メインコンテンツに対して少なくとも1つの`media.play` イベントが受信されたセグメントをカバーする任意のクローズコールに対して`mediaReporting.sessionDetails.hasSegmentView = true`を設定します。 この指標は、クローズ呼び出しで報告されます。 Media Edge API パスでは、セグメントビューはコンテンツの開始と同じ条件で実行されます。 どちらも、メインコンテンツに`media.play`が必要です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.segmentView`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
