---
title: 推定ストリーム
description: セッションあたりのオーディオまたはビデオストリームの数を概算します。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 10%

---


# 推定ストリーム

**推定ストリーム**&#x200B;指標は、セッションあたりのオーディオまたはビデオストリームの数を近似し、合計再生時間が30分ごとに1つのストリームをカウントします。 これは、コンテンツシンジケーション契約と、消費の各30分ブロックが個別の「ストリーム」としてカウントされるリーチ近似を目的としています。

## この指標の計算方法

メディアバックエンドは、この指標を`FLOOR(totalTimePlayed / 1800) + 1`として計算します。この指標は、`totalTimePlayed`が[&#x200B; メディア滞在時間](media-time-spent.md)秒単位です。 この指標は、クローズ呼び出しで報告されます。

| メディア滞在時間 | 推定ストリーム |
| --- | --- |
| 0～29分 | 1 |
| 30～59分 | 2 |
| 60～89分 | 3 |
| 90分以上 | 4+ |

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.estimatedStreams`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.estimatedStreams`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
