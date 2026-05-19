---
title: 推定ストリーム
description: セッションあたりのオーディオまたはビデオストリームの数を概算します。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 10%

---


# 推定ストリーム

**推定ストリーム**&#x200B;指標は、セッションあたりのオーディオまたはビデオストリームの数を近似し、合計再生時間が30分ごとに1つのストリームをカウントします。 これは、コンテンツシンジケーション契約と、消費の各30分ブロックが個別の「ストリーム」としてカウントされるリーチ近似を目的としています。

## この指標の計算方法

メディアバックエンドは`mediaReporting.sessionDetails.estimatedStreams = FLOOR(totalTimePlayed / 1800) + 1`を計算します。ここで、`totalTimePlayed`は[&#x200B; メディア滞在時間](media-time-spent.md)秒です。 この指標は、クローズ呼び出しで報告されます。

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
