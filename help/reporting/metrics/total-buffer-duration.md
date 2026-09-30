---
title: 合計バッファー時間（指標）
description: セッション間の合計と平均の累積バッファー時間をレポートします。
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
source-wordcount: '196'
ht-degree: 7%
---

# 合計バッファー時間（指標）

>[!BEGINSHADEBOX]

*このページでは、**合計バッファ時間**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferTime`個のコンテキストデータ変数から、ペアの[合計バッファー期間（ディメンション） &#x200B;](/help/reporting/dimensions/total-buffer-duration.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.bufferTime` フィールドを公開します。*

>[!ENDSHADEBOX]

**合計バッファー時間**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間の累積バッファー時間をレポートします。 この指標を使用して、レポート期間中に顧客がバッファーを待機した合計時間を計算します。

## この指標の計算方法

メディアバックエンドは、各バッファー間隔のデュレーションを合計します（[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)から次の状態変更まで）。 この指標は、クローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferTime`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
