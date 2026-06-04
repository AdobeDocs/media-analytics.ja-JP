---
title: ドロップされたフレーム （指標）
description: セッション間の合計と平均の累積ドロップ済みフレームをレポートします。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# ドロップされたフレーム （指標）

>[!BEGINSHADEBOX]

*このページでは、**削除されたフレーム**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.droppedFrameCount` コンテキストデータ変数からペアの[&#x200B; ドロップされたフレーム（ディメンション） &#x200B;](/help/reporting/dimensions/dropped-frames.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.droppedFrames` フィールドを公開します。 この変数の収集方法については、[削除されたフレーム &#x200B;](/help/implementation/variables/quality/dropped-frames.md)を参照してください。*

>[!ENDSHADEBOX]

**ドロップフレーム**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間の累積ドロップフレームをレポートします。 この指標を使用して、レポート期間の合計配信数を計算し、コンテンツ、ネットワーク、プレーヤー間のフレームレンダリング品質を比較します。

## この指標の計算方法

ドロップが蓄積すると、プレーヤーはQoE オブジェクトの`droppedFrames`値を更新します。 バックエンドは、クローズコールの最新の値をレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.droppedFrameCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

セッションレベルのブール値レポートの場合（任意のフレームがドロップされたかどうかにかかわらず）、[&#x200B; ドロップされたフレームの影響を受けるストリーム &#x200B;](dropped-frame-impacted-streams.md)を使用します。
