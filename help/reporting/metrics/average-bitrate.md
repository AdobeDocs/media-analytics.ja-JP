---
title: 平均ビットレート（指標）
description: 各セッションの生の重み付け平均ビットレートをkbpsでレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 7%

---


# 平均ビットレート（指標）

>[!BEGINSHADEBOX]

*このページでは、**平均ビットレート**イベント指標について説明します。この指標は、セッションあたりの生の加重平均ビットレートを報告します。 グループ化されたディメンションについては、[平均ビットレート （ディメンション） ](/help/reporting/dimensions/average-bitrate.md)を参照してください。 この変数の収集方法については、[ ビットレート ](/help/implementation/variables/quality/bitrate.md)を参照してください。*

>[!ENDSHADEBOX]

**平均ビットレート**&#x200B;指標は、各セッションの生の加重平均再生ビットレート（kbps）をレポートします。 [ バケット ディメンション ](/help/reporting/dimensions/average-bitrate.md)とは異なり、指標は、合計、平均、およびセッション間のパーセンタイル ロールアップに適した連続的な数値です。

## この指標の計算方法

メディアバックエンドは、セッション中に報告されたすべてのビットレート値の重み付け平均を計算し、各ビットレートがアクティブだった期間で重み付けします。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateAverage`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
