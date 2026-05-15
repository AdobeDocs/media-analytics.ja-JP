---
title: 影響を受けるストリームを一時停止しました
description: ビューアが少なくとも1回一時停止したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 11%

---


# 影響を受けるストリームを一時停止しました

**一時停止された影響を受けるストリーム**&#x200B;指標では、ビューアが少なくとも1回一時停止したセッションがカウントされます。 セッションレベルのブール値です。 同じセッション内の複数の一時停止は、影響を受ける1つのストリームとしてカウントされます。 一時停止が発生したセッションの割合を測定するために使用します。合計一時停止ボリュームには、[一時停止イベント ](pause-events.md)を使用します。

## この指標の計算方法

メディア バックエンドは、セッション中に[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントを初めて受信したときに`mediaReporting.sessionDetails.hasPauseImpactedStreams = true`を設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.pause`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
