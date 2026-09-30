---
title: コンテンツ完了
description: 再生ヘッドがコンテンツの最後に達したセッションをカウントします。
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
source-wordcount: '142'
ht-degree: 10%
---

# コンテンツ完了

**コンテンツが完了しました**&#x200B;指標は、再生ヘッドがコンテンツの最後に達したセッションをカウントします。 [&#x200B; コンテンツ開始](content-starts.md)と組み合わせて完了率を計算し、[&#x200B; メディア開始](media-starts.md)と組み合わせてエンドツーエンドの表示率を計算します。

## この指標の計算方法

メディアバックエンドは、[&#x200B; セッション完了](/help/implementation/events/session/session-complete.md) イベントを受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。 明示的な`sessionComplete`なしでタイムアウトしたセッションは、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.complete` |
