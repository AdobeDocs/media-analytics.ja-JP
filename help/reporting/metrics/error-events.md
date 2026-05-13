---
title: エラーイベント
description: セッション全体の合計と平均のエラーイベントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 7%

---


# エラーイベント

>[!BEGINSHADEBOX]

*このページでは、**エラーイベント**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.errorCount`個のコンテキストデータ変数から、ペアの[&#x200B; エラーディメンション &#x200B;](/help/reporting/dimensions/errors.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.errorCount` フィールドを公開します。*

>[!ENDSHADEBOX]

**エラーイベント**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間のエラーイベントをカウントします。 この指標を使用して、レポート期間中の合計エラー量を計算し、コンテンツ、ネットワーク、プレーヤー間のエラー率を比較します。

## この指標の計算方法

メディアバックエンドは、プレーヤーによって報告されるすべてのエラーのカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.errorCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |

セッションレベルのブール値レポートの場合（エラーが発生したかどうかにかかわらず）、[&#x200B; エラーが影響を受けるストリーム &#x200B;](error-impacted-streams.md)を使用します。
