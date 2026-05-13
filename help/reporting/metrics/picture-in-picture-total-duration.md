---
title: ピクチャインピクチャの合計時間
description: ビューアがセッション中にピクチャインピクチャに費やした累積秒数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 6%

---


# ピクチャインピクチャの合計時間

>[!BEGINSHADEBOX]

*このページでは、**ピクチャーの合計期間**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[図](/help/implementation/variables/player-state/picture-in-picture.md)を参照してください。*

>[!ENDSHADEBOX]

**ピクチャインピクチャの合計時間**&#x200B;指標は、視聴者がセッション中にピクチャインピクチャで費やした累積時間（秒単位）を報告します。 バックエンドは、ピクチャ・イン・ピクチャ状態の開始と一致する状態の終了イベントとの間のすべての間隔を合計する。

## この指標の計算方法

メディアバックエンドは、セッション中にすべてのピクチャインピクチャのインターバルで経過した時間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.pictureinpicture.time`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "pictureInPicture"`、フィールド `time`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
