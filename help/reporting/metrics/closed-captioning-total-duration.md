---
title: クローズドキャプションの合計期間
description: セッション中に累積秒キャプションが有効になったことをレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 7%

---


# クローズドキャプションの合計期間

>[!BEGINSHADEBOX]

*このページでは、**クローズドキャプションの合計期間**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[&#x200B; クローズドキャプション &#x200B;](/help/implementation/variables/player-state/closed-captioning.md)を参照してください。*

>[!ENDSHADEBOX]

**クローズドキャプションの合計期間**&#x200B;指標は、セッション中にキャプションが有効になった累積時間を秒単位で報告します。 バックエンドは、キャプションイネーブル状態の開始と一致する状態の終了イベントとの間のすべての間隔を合計します。

## この指標の計算方法

メディアバックエンドは、セッション中にキャプションが有効なすべての間隔で経過した時間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.closedcaptioning.time`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "closedCaptioning"`、フィールド `time`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
