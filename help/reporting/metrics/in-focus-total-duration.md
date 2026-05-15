---
title: フォーカスの合計時間
description: セッション中にプレイヤーがフォーカスしていた累積秒数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# フォーカスの合計時間

>[!BEGINSHADEBOX]

*このページでは、**フォーカス合計期間**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[&#x200B; フォーカス中](/help/implementation/variables/player-state/in-focus.md)を参照してください。*

>[!ENDSHADEBOX]

**フォーカスの合計時間**&#x200B;指標は、セッション中にプレーヤーがフォーカスに入った累積時間を秒単位で報告します。 バックエンドは、フォーカス状態の開始と一致する状態の終了イベントとの間の間隔を合計する。

## この指標の計算方法

メディアバックエンドは、セッション中にすべてのフォーカス間隔で経過した時間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.infocus.time`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "inFocus"`、フィールド `time`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
