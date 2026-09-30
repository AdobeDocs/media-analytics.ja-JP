---
title: バッファーイベント（ディメンション）
description: セッションごとのバッファリングイベントの数を報告します。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 8%
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
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## ディメンション項目

各アイテムは、クローズ呼び出しで報告されるリテラルのバッファーカウント値です。 セッションレベルのブール値レポートの場合（セッションでバッファリングが発生したかどうかに関係なく）、[影響を受けるストリームのバッファリング &#x200B;](/help/reporting/metrics/buffer-impacted-streams.md)を使用します。
