---
title: 合計バッファー時間（指標）
description: セッション間の合計と平均の累積バッファー時間をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# 合計バッファー時間（指標）

>[!BEGINSHADEBOX]

*このページでは、**合計バッファ時間**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferTime`個のコンテキストデータ変数から、ペアの[合計バッファー期間（ディメンション） &#x200B;](/help/reporting/dimensions/total-buffer-duration.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.bufferTime` フィールドを公開します。*

>[!ENDSHADEBOX]

**合計バッファー時間**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間の累積バッファー時間をレポートします。 この指標を使用して、レポート期間中に顧客がバッファーを待機した合計時間を計算します。

## この指標の計算方法

メディアバックエンドは、各バッファー間隔（`media.bufferStart`から次の状態変更まで）の期間を合計します。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferTime`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
