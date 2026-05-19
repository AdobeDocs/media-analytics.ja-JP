---
title: ミュート数
description: セッション中に視聴者がオーディオをミュートした回数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# ミュート数

>[!BEGINSHADEBOX]

*このページでは、**分数**&#x200B;レポート指標について説明します。 この変数の収集方法については、[Mute](/help/implementation/variables/player-state/mute.md)を参照してください。*

>[!ENDSHADEBOX]

**ミュート数**&#x200B;指標は、セッション中に視聴者がオーディオをミュートした回数を報告します。 ミュート状態の開始イベントごとにカウントが増加します。 セッションレベルのブール値ロールアップでミュート [&#128279;](mute-streams-impacted.md)の影響を受ける ストリームと、状態の合計時間で[&#x200B; ミュート合計時間](mute-total-duration.md)を組み合わせます。

## この指標の計算方法

メディアバックエンドでは、ミュート状態の開始イベントごとに、このカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.mute.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "mute"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
