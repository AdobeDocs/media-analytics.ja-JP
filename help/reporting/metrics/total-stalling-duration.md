---
title: 合計滞留時間
description: セッション全体の合計と平均の累積失敗時間をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# 合計滞留時間

**合計ストール期間**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間の累積失敗時間をレポートします。 この指標を使用して、レポート期間に停止した再生待ちに視聴者が費やした合計時間を計算します。

Customer Journey Analyticsでは、`xdm.mediaReporting.qoeDataDetails.stallTime`を指標として使用することも、ディメンションのコンポーネントを別個にすることなくディメンションとして使用することもできます。

## この指標の計算方法

メディアバックエンドは、少なくとも3つの連続したイベントについて再生ヘッドの動きがメインコンテンツに記録されていない場合に検出される各停止間隔の時間を合計する。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stallTime`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.qoe.stallTime`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
