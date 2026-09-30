---
title: フォーカス数
description: セッション中にプレイヤーがフォーカスを得た回数を報告します。
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
source-wordcount: '165'
ht-degree: 9%
---

# フォーカス数

>[!BEGINSHADEBOX]

*このページでは、**フォーカス数**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[&#x200B; フォーカス中](/help/implementation/variables/player-state/in-focus.md)を参照してください。*

>[!ENDSHADEBOX]

**インフォーカス カウント**&#x200B;指標は、セッション中にプレイヤーがフォーカスを得た回数を報告します。 各フォーカス状態の開始イベントは、カウントを増分します。 セッションレベルのブール値ロールアップでは[&#x200B; フォーカスの影響を受けるストリーム &#x200B;](in-focus-streams-impacted.md)と、状態での合計時間では[&#x200B; フォーカスの合計時間](in-focus-total-duration.md)と組み合わせます。

## この指標の計算方法

メディアバックエンドでは、フォーカスステータス開始イベントごとに、このカウントを増加させます。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.states.infocus.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "inFocus"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
