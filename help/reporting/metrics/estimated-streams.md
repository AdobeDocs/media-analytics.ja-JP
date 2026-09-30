---
title: 推定ストリーム
description: セッションあたりのオーディオまたはビデオストリームの数を概算します。
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
| Adobe Analytics | `a.media.estimatedStreams`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.estimatedStreams`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
