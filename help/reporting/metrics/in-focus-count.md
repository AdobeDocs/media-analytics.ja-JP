---
title: フォーカス数
description: セッション中にプレイヤーがフォーカスを得た回数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# フォーカス数

>[!BEGINSHADEBOX]

*このページでは、**フォーカス数**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[&#x200B; フォーカス中](/help/implementation/variables/player-state/in-focus.md)を参照してください。*

>[!ENDSHADEBOX]

**インフォーカス カウント**&#x200B;指標は、セッション中にプレイヤーがフォーカスを得た回数を報告します。 各フォーカス状態の開始イベントは、カウントを増分します。 セッションレベルのブール値ロールアップでは[&#x200B; フォーカスの影響を受けるストリーム &#x200B;](in-focus-streams-impacted.md)と、状態での合計時間では[&#x200B; フォーカスの合計時間](in-focus-total-duration.md)と組み合わせます。

## この指標の計算方法

メディアバックエンドは、フォーカス状態の開始イベントごとに`mediaReporting.states[]`の`inFocus` エントリの`count` フィールドを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.infocus.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "inFocus"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
