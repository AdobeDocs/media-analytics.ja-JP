---
title: 合計期間をミュート
description: セッション中にオーディオがミュートされた累積秒数を報告します。
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
source-wordcount: '167'
ht-degree: 8%
---

# 合計期間をミュート

>[!BEGINSHADEBOX]

*このページでは、**合計期間**のレポート指標について説明します。 この変数の収集方法については、[Mute](/help/implementation/variables/player-state/mute.md)を参照してください。*

>[!ENDSHADEBOX]

**ミュート合計時間**&#x200B;指標は、セッション中にオーディオがミュートされた累積時間を秒単位で報告します。 バックエンドは、ミュート状態の開始イベントと一致する状態の終了イベントとの間の間隔を合計する。

## この指標の算出方法

メディアバックエンドは、セッション中のすべてのミュート間隔で経過した時間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.states.mute.time`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "mute"`、フィールド `time`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.mute.time` |
