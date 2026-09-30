---
title: 認証済み
description: Adobe Passを通じてユーザーが承認されたセッションをカウントします。
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
source-wordcount: '137'
ht-degree: 12%
---

# 認証済み

>[!BEGINSHADEBOX]

*このページでは、**承認済み**&#x200B;レポート指標について説明します。 この変数の収集方法については、[Authorized](/help/implementation/variables/standard-metadata/authorized.md)を参照してください。*

>[!ENDSHADEBOX]

**Authorized**&#x200B;指標は、Adobe PassまたはTV-Everywhereを通じてユーザーが承認されたセッションをカウントします。 [MVPD](/help/reporting/dimensions/mvpd.md) ディメンションと組み合わせて、プロバイダーごとの認証ボリュームを分割します。

## この指標の計算方法

メディアバックエンドは、セッション開始時にプレーヤーがセッションを「許可された」とフラグ付けしたときにカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.pass.auth`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
