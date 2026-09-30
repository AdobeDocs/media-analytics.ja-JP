---
title: メディア開始
description: プリロール広告またはバッファリングで終了したセッションを含め、開始されたすべてのメディアセッションをカウントします。
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
source-wordcount: '228'
ht-degree: 6%
---

# メディア開始

**メディア開始**&#x200B;指標は、開始されたすべてのメディアセッションをカウントします。 プレロール広告、バッファリング、またはメインコンテンツの再生前にビューアが脱落した場合でも、バックエンドが[&#x200B; セッション開始](/help/implementation/events/session/session-start.md) イベントを受信するとすぐに増分されます。 この指標は、メディアレポートで最も広いfunnel上部の指標として使用します。広告とバッファーのドロップオフを測定するために、[Content starts](content-starts.md)と組み合わせます。

## この指標の計算方法

メディアバックエンドは、[&#x200B; セッション開始](/help/implementation/events/session/session-start.md) イベントを受信したときに、このフラグを設定します。 報告された指標は、セッションごとに`1`です。 メディアの開始は、クローズ呼び出しではなく開始呼び出しで報告されます。セッションのクローズを待たない唯一の指標です。 [&#x200B; コンテンツ開始](/help/reporting/metrics/content-starts.md)、[&#x200B; コンテンツ滞在時間](/help/reporting/metrics/content-time-spent.md)、[&#x200B; プログレスマーカー](/help/reporting/metrics/progress-markers.md)など、その他のすべてのメディア指標は、クローズコールで報告され、再生中にリアルタイムでは使用できません。 [広告開始](/help/reporting/metrics/ad-starts.md)は、クローズ時ではなく、トリガーイベントで報告される1つの追加指標です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.view`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.view` |
