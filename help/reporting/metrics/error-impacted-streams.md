---
title: エラーの影響を受けるストリーム
description: 少なくとも1つのエラーが発生したセッションをカウントします。
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
source-wordcount: '143'
ht-degree: 10%
---

# エラーの影響を受けるストリーム

**エラーの影響を受けたストリーム**&#x200B;指標では、少なくとも1つのエラーが発生したセッションをカウントします（`trackError`が呼び出されたか、[ エラー](/help/implementation/events/error.md) イベントが発生しました）。 この指標はセッションレベルのブール値です。同じセッション内の複数のエラーは、影響を受ける1つのストリームとしてカウントされます。 合計エラーボリュームには、[ エラー](/help/reporting/dimensions/errors.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に[ エラー](/help/implementation/events/error.md) イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.error`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
