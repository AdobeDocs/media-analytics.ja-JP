---
title: 全画面表示の合計時間
description: セッション中にビューアがフルスクリーンで費やした累積秒数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 全画面表示の合計時間

>[!BEGINSHADEBOX]

*このページでは、**全画面表示の合計期間**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[全画面](/help/implementation/variables/player-state/full-screen.md)を参照してください。*

>[!ENDSHADEBOX]

**フルスクリーン合計時間**&#x200B;指標は、視聴者がセッション中にフルスクリーンで費やした累積時間を秒単位で報告します。 バックエンドは、フルスクリーン状態の開始と一致する状態の終了イベントの間のすべての間隔を合計します。

## この指標の計算方法

メディアバックエンドは、セッション中にすべてのフルスクリーン間隔で経過した時間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.fullscreen.time`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "fullscreen"`、フィールド `time`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
