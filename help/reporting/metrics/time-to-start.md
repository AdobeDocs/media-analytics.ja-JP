---
title: 開始時間（指標）
description: セッション全体の合計と平均の起動時間をレポートします。
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
source-wordcount: '202'
ht-degree: 7%
---

# 開始時間（指標）

>[!BEGINSHADEBOX]

*このページでは、**開始時間**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.timeToStart`個のコンテキストデータ変数から、ペアの[開始時間（ディメンション） &#x200B;](/help/reporting/dimensions/time-to-start.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.timeToStart` フィールドを公開します。 この変数の収集方法については、[開始時間](/help/implementation/variables/quality/time-to-start.md)を参照してください。*

>[!ENDSHADEBOX]

**開始時間**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間の起動時間をレポートします。 この指標を使用して、レポート期間の平均起動時間を計算し、コンテンツ、ネットワーク、プレーヤー間の起動パフォーマンスを比較します。 Adobeは、値を秒単位で保存し、取り込み時にプレーヤーがレポートするミリ秒単位からコンバージョンします。

## この指標の計算方法

セッションが開始される前に、プレーヤーはQoE オブジェクトに`timeToStart`を設定します。 バックエンドは、クローズコールの値をレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.timeToStart`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
