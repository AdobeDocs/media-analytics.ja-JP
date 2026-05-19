---
title: 章数
description: セッション中に開始したチャプターの数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 9%

---


# 章数

**チャプター数**&#x200B;指標は、セッション中に開始したチャプターの数を報告します。 章の消費量をコンテンツ間で比較するために使用します。 チャプターディメンション（チャプター名、位置）でピボットされたチャプター開始カウントの場合は、チャプター変数カテゴリが有効になっている場合に使用できるチャプタースタート指標を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に受信した[章開始](/help/implementation/events/chapters/chapter-start.md) イベントごとに、このカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.chapterCount`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.chapterCount`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | 該当なし |
