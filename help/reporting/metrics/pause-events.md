---
title: イベントを一時停止
description: セッション中に発生したすべての個別の一時停止をカウントします。
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
source-wordcount: '170'
ht-degree: 10%
---

# イベントを一時停止

**一時停止イベント**&#x200B;指標は、同じセッション内の複数の一時停止を含め、セッション中に受信された個別の[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントをすべてカウントします。 [合計一時停止デュレーション ](total-pause-duration.md)と組み合わせて平均一時停止の長さを導き出し、[影響を受けるストリーム ](paused-impacted-streams.md)と組み合わせて、少なくとも1回一時停止したセッションをカウントします。

## この指標の計算方法

メディアバックエンドでは、[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントごとに、このカウントが増加します。 1回の連続した一時停止では、時間に関係なく1回の増分が生成されます。 プレーヤーが一時停止したままの間に送信されたハートビート [ping](/help/implementation/events/playback/ping.md)はすべて同じ一時停止ピリオドに属しており、カウントを再度増加させません。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.pauseCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
