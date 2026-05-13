---
title: エラーの影響を受けるストリーム
description: 少なくとも1つのエラーが発生したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 9%

---


# エラーの影響を受けるストリーム

**エラーが影響を受けたストリーム**&#x200B;指標では、少なくとも1つのエラーが発生したセッションをカウントします（`trackError`が呼び出されたか、`media.error` イベントが発生しました）。 この指標はセッションレベルのブール値で、同じセッション内の複数のエラーが、影響を受ける1つのストリームとしてカウントされます。 合計エラーボリュームには、[&#x200B; エラー](/help/reporting/dimensions/errors.md)を使用します。

## この指標の計算方法

メディア バックエンドは、セッション中に`media.error` イベントを初めて受信したときに`mediaReporting.qoeDataDetails.hasErrorImpactedStreams = true`を設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.error`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
