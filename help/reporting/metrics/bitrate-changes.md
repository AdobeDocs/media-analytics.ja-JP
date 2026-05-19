---
title: ビットレートの変更（指標）
description: セッション全体の合計と平均のビットレート変更イベントをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# ビットレートの変更（指標）

>[!BEGINSHADEBOX]

*このページでは、**ビットレートの変更**&#x200B;指標について説明します。 Adobe Analyticsは、同じ`a.media.qoe.bitrateChangeCount`個のコンテキストデータ変数から、ペアの[&#x200B; ビットレート変更（ディメンション） &#x200B;](/help/reporting/dimensions/bitrate-changes.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.bitrateChangeCount` フィールドを公開します。 ビットレート変更イベントを実行する方法については、[&#x200B; ビットレート変更](/help/implementation/variables/quality/bitrate-change.md)を参照してください。*

>[!ENDSHADEBOX]

**ビットレート変更**&#x200B;指標では、合計、平均、パーセンタイルのロールアップに適した、セッション間のビットレート変更イベントがカウントされます。 この指標を使用して、レポート期間のビットレート変更量の合計を計算し、コンテンツ、ネットワーク、プレーヤー間のビットレートの安定性を比較します。

## この指標の計算方法

メディアバックエンドは、セッション中に受信した[&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md) イベントごとにカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateChangeCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

セッションレベルのブール値レポートの場合（セッションでビットレートの変更が発生したかどうかにかかわらず）、[&#x200B; ビットレートの変更が影響を受けるストリーム &#x200B;](bitrate-change-impacted-streams.md)を使用します。
