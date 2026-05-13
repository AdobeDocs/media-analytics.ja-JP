---
title: ビットレートの変更が影響を受けるストリーム
description: 少なくとも1つのビットレート変更が発生したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# ビットレートの変更が影響を受けるストリーム

**ビットレートの変更が影響を受けたストリーム**&#x200B;指標では、少なくとも1つのビットレートの変更が発生したセッションがカウントされます。 この指標はセッションレベルのブール値で、影響を受ける1つのストリームと同じセッション数の中で複数のビットレート変更が発生します。 総ビットレート変更ボリュームに対して、[&#x200B; ビットレート変更](/help/reporting/dimensions/bitrate-changes.md)を使用します。

## この指標の計算方法

メディア バックエンドは、セッション中に`media.bitrateChange` イベントを初めて受信したときに`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true`を設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateChange`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
