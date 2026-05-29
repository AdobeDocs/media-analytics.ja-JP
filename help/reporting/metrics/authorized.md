---
title: 認証済み
description: Adobe Passを通じてユーザーが承認されたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.pass.auth`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
