---
title: 章の滞在時間
description: 章ごとのアクティブな再生の合計秒数を報告します。
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
source-wordcount: '156'
ht-degree: 9%
---

# 章の滞在時間

**章の滞在時間**&#x200B;指標は、章ごとのアクティブな再生の合計秒数を報告します。 [章の長さ](/help/reporting/dimensions/chapter-length.md)と組み合わせて、消費された各章のシェアを計算します。

## この指標の計算方法

メディアバックエンドは、プレーヤーがチャプターの`play`状態にある間に、イベント間の経過時間を合計します。 一時停止、バッファリング、ストール中の時間は除外されます。 この指標は、章のクローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディアチャプター]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.chapter.timePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
