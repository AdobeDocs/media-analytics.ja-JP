---
title: 影響を受けるストリームを停止する
description: 再生中に少なくとも1回のストールが発生したセッションをカウントします。
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
source-wordcount: '178'
ht-degree: 8%
---

# 影響を受けるストリームを停止する

**失速の影響を受けるストリーム**&#x200B;指標は、再生中に少なくとも1回の失速が発生したセッションをカウントします。 この指標はセッションレベルのブール値です。同じセッション内の複数のストールは、影響を受ける1つのストリームとしてカウントされます。 合計失速ボリュームには、[失速イベント &#x200B;](stall-events.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に少なくとも3つの連続したイベントについて、メインコンテンツに再生ヘッドの動きが記録されていない場合に、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stall`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.qoe.stall`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
