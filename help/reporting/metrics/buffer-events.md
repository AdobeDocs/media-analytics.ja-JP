---
title: バッファーイベント（指標）
description: セッション全体の合計と平均のバッファリングイベントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# バッファーイベント（指標）

>[!BEGINSHADEBOX]

*このページでは、**バッファーイベント**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferCount`個のコンテキストデータ変数から、ペアの[&#x200B; バッファーイベント（ディメンション） &#x200B;](/help/reporting/dimensions/buffer-events.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.bufferCount` フィールドを公開します。*

>[!ENDSHADEBOX]

**バッファーイベント**&#x200B;指標は、合計、平均、パーセンタイルのロールアップに適した、セッション間のバッファリングイベントをカウントします。 この指標を使用して、レポート期間の合計バッファー量を計算し、コンテンツ、ネットワーク、プレーヤー間のバッファー安定性を比較します。

## この指標の計算方法

メディアバックエンドは、プレーヤーが[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)状態に入るたびにカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

セッションレベルのブール値レポートの場合（セッションでバッファリングが発生したかどうかに関係なく）、[影響を受けるストリームのバッファリング &#x200B;](buffer-impacted-streams.md)を使用します。
