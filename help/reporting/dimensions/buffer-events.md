---
title: バッファーイベント（ディメンション）
description: セッションごとのバッファリングイベントの数を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# バッファーイベント（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**バッファーイベント**&#x200B;ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferCount`個のコンテキストデータ変数から、ペアの[&#x200B; バッファーイベント（指標） &#x200B;](/help/reporting/metrics/buffer-events.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.bufferCount` フィールドを公開します。*

>[!ENDSHADEBOX]

**バッファーイベント** ディメンションは、セッション中に発生したバッファリングイベントの数を報告します。 ディメンションを使用して、正確なバッファー数ごとにエンゲージメントを分割します。

## このディメンションの入力方法

メディアバックエンドでは、プレーヤーが`buffer`状態になるたびにカウントが増加します。 値はクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## ディメンション項目

各アイテムは、クローズ呼び出しで報告されるリテラルのバッファーカウント値です。 セッションレベルのブール値レポートの場合（セッションでバッファリングが発生したかどうかに関係なく）、[影響を受けるストリームのバッファリング &#x200B;](/help/reporting/metrics/buffer-impacted-streams.md)を使用します。
