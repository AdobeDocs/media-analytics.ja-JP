---
title: 影響を受けるストリームを一時停止しました
description: ビューアが少なくとも1回一時停止したセッションをカウントします。
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
source-wordcount: '152'
ht-degree: 11%
---

# 影響を受けるストリームを一時停止しました

**一時停止された影響を受けるストリーム**&#x200B;指標では、ビューアが少なくとも1回一時停止したセッションがカウントされます。 セッションレベルのブール値です。 同じセッション内の複数の一時停止は、影響を受ける1つのストリームとしてカウントされます。 一時停止が発生したセッションの割合を測定するために使用します。合計一時停止ボリュームには、[一時停止イベント &#x200B;](pause-events.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.pause`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
