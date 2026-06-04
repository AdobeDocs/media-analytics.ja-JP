---
title: エラーイベント
description: セッション全体の合計と平均のエラーイベントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# エラーイベント

>[!BEGINSHADEBOX]

*このページでは、**エラーイベント**指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.errorCount`個のコンテキストデータ変数から、ペアの[ エラーディメンション ](/help/reporting/dimensions/errors.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.errorCount` フィールドを公開します。*

>[!ENDSHADEBOX]

**エラーイベント**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間のエラーイベントをカウントします。 この指標を使用して、レポート期間中の合計エラー量を計算し、コンテンツ、ネットワーク、プレーヤー間のエラー率を比較します。

## この指標の計算方法

メディアバックエンドは、プレーヤーによって報告されるすべてのエラーのカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.errorCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

セッションレベルのブール値レポートの場合（エラーが発生したかどうかにかかわらず）、[ エラーが影響を受けるストリーム ](error-impacted-streams.md)を使用します。
