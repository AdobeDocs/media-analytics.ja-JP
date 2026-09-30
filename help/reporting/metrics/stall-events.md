---
title: ストールイベント
description: セッション全体の合計と平均のストールイベントをカウントします。
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
source-wordcount: '203'
ht-degree: 7%
---

# ストールイベント

**ストールイベント**&#x200B;指標では、合計、平均、パーセンタイルのロールアップに適した、セッション間のストールイベントがカウントされます。 この指標を使用して、レポート期間中の合計失速ボリュームを計算し、コンテンツ、ネットワーク、プレーヤー間の失速の安定性を比較します。

Customer Journey Analyticsでは、`xdm.mediaReporting.qoeDataDetails.stallCount`を指標として使用することも、ディメンションのコンポーネントを別個にすることなくディメンションとして使用することもできます。

## この指標の計算方法

メディアバックエンドは、少なくとも3つの連続したイベントについて、再生ヘッドの移動がメインコンテンツに記録されるたびにカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stallCount`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.qoe.stallCount`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

セッションレベルのブール値レポートの場合（ストールが発生したかどうかにかかわらず）、[影響を受けるストリームをストール &#x200B;](stall-impacted-streams.md)します。
