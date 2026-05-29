---
title: 章の滞在時間
description: 章ごとのアクティブな再生の合計秒数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | [[!UICONTROL &#x200B; メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.timePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
