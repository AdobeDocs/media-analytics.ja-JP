---
title: イベントを一時停止
description: セッション中に発生したすべての個別の一時停止をカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# イベントを一時停止

**一時停止イベント**&#x200B;指標は、同じセッション内の複数の一時停止を含め、セッション中に受信された個別の[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントをすべてカウントします。 [合計一時停止デュレーション &#x200B;](total-pause-duration.md)と組み合わせて平均一時停止の長さを導き出し、[影響を受けるストリーム &#x200B;](paused-impacted-streams.md)と組み合わせて、少なくとも1回一時停止したセッションをカウントします。

## この指標の計算方法

メディアバックエンドでは、[一時停止の開始](/help/implementation/events/playback/pause-start.md) イベントごとに、このカウントが増加します。 1回の連続した一時停止では、時間に関係なく1回の増分が生成されます。 プレーヤーが一時停止したままの間に送信されたハートビート [ping](/help/implementation/events/playback/ping.md)はすべて同じ一時停止ピリオドに属しており、カウントを再度増加させません。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.pauseCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
