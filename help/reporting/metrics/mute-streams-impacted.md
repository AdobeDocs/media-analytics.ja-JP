---
title: ミュートの影響を受けるストリーム
description: ビューアが少なくとも1回オーディオをミュートしたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# ミュートの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、ミュート&#x200B;**レポート指標の影響を受ける**&#x200B;ストリームについて説明します。 この変数の収集方法については、[Mute](/help/implementation/variables/player-state/mute.md)を参照してください。*

>[!ENDSHADEBOX]

ミュート **指標の影響を受ける** ストリームでは、ビューアが少なくとも1回オーディオをミュートしたセッションがカウントされます。 この指標はセッションレベルのブール値です。影響を受ける1つのストリームと同じセッション数内の複数のミュートトグルです。 ミュートの合計数には、[&#x200B; ミュート数](mute-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中にミュート状態の開始イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.mute.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "mute"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
