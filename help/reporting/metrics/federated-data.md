---
title: 連合データ
description: 顧客独自の実装ではなく、連合データ共有を介して受信したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 6%

---


# 連合データ

>[!AVAILABILITY]
>
>Federated Analytics サービスは、Adobe Analyticsでストリーミングメディア機能を使用する場合にのみ使用できます。 Federated AnalyticsはCustomer Journey Analyticsでは使用できません。

**フェデレーションデータ**&#x200B;指標は、独自の実装からではなく、フェデレーションデータ共有を介して受信されたセッションをカウントします。 パートナーが共有するセッションの量を測定し、エンゲージメント、完了率、品質をファーストパーティセッションと比較するために使用します。

詳しくは、[Federated Media](/help/use-cases/federated-media.md)の使用例を参照してください。

>[!TIP]
>
>連合データをディメンションとして使用する場合は、`a.media.federated`個のコンテキストデータ変数をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。

## この指標の計算方法

セッションがフェデレーションチャネル経由で受信されると、メディアバックエンドは`mediaReporting.sessionDetails.isFederated = true`を設定します。 この指標は、適格セッションごとに1回増加し、クローズコールで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.federated`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.federated` |
