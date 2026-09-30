---
title: 広告数
description: セッション中に開始された広告の数をレポートします。
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
source-wordcount: '176'
ht-degree: 9%
---

# 広告数

**広告数**&#x200B;指標は、セッション中に開始された広告の数を報告します。 このツールを使用して、コンテンツ、チャネル、ストリームタイプごとの広告ロードを把握します。 広告ディメンション（広告主、キャンペーン、クリエイティブ）によってピボット化された広告開始数の場合は、広告変数カテゴリが有効になっている場合に使用できる広告開始指標を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に受信した[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとに、このカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.adCount`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.adCount`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | 該当なし |
