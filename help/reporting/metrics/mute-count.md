---
title: ミュート数
description: セッション中に視聴者がオーディオをミュートした回数をレポートします。
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
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.states.mute.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "mute"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
