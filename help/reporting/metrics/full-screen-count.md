---
title: 全画面数
description: セッション中にビューアがフルスクリーンに入った回数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# 全画面数

>[!BEGINSHADEBOX]

*このページでは、**全画面数**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[全画面](/help/implementation/variables/player-state/full-screen.md)を参照してください。*

>[!ENDSHADEBOX]

**全画面数**&#x200B;指標は、視聴者がセッション中に全画面表示に入った回数を報告します。 全画面表示の状態開始イベントごとにカウントが増加します。 セッションレベルのブール値ロールアップでは[&#x200B; フルスクリーンの影響を受けるストリーム &#x200B;](full-screen-streams-impacted.md)と、状態での合計時間では[&#x200B; フルスクリーン合計時間](full-screen-total-duration.md)と組み合わせます。

## この指標の計算方法

メディアバックエンドでは、全画面表示の状態スタートイベントごとに、このカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.fullscreen.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "fullscreen"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
