---
title: コンテンツの再開
description: 以前に中断された再生を再開したセッションをカウントします。
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
source-wordcount: '171'
ht-degree: 9%
---

# コンテンツの再開

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ再開**&#x200B;レポート指標について説明します。 この変数の収集方法については、[&#x200B; コンテンツの再開](/help/implementation/variables/core/content-resumes.md)を参照してください。*

>[!ENDSHADEBOX]

**Content resumes**&#x200B;指標は、以前に中断された再生を再開したセッションをカウントします。 プレーヤーがセッションを`sessionStart`の再開としてフラグ付けすると、増分されます（たとえば、バッファー、一時停止、失速が30分を超えた後など）。 同じビューアとアセットの継続セッションから本物の新しいセッションを分離するために使用します。

## この指標の計算方法

メディアバックエンドは、`xdm.mediaCollection.sessionDetails.hasResume`が[&#x200B; セッション開始](/help/implementation/events/session/session-start.md) イベントの`true`の場合にこのフラグを設定します。 プレーヤーは、セッションに履歴書として明示的にフラグを付ける必要があります。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.resume`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | 該当なし |
