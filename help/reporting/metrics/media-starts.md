---
title: メディア開始
description: プリロール広告またはバッファリングで終了したセッションを含め、開始されたすべてのメディアセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# メディア開始

**メディア開始**&#x200B;指標は、開始されたすべてのメディアセッションをカウントします。 プレロール広告、バッファリング、またはメインコンテンツの再生前にビューアが脱落しても、バックエンドが`media.sessionStart` イベントを受信するとすぐに増分されます。 この指標は、メディアレポートで最も広いfunnel上部の指標として使用します。広告とバッファーのドロップオフを測定するために、[Content starts](content-starts.md)と組み合わせます。

## この指標の計算方法

メディア バックエンドは、`media.sessionStart` イベントを受信したときに`mediaReporting.sessionDetails.isViewed = true`を設定します。 報告された指標は、セッションごとに`1`です。 メディアの開始は、クローズ呼び出しではなく、開始呼び出しで報告されます。 セッションのクローズを待たない唯一のフェーズ 1指標です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
