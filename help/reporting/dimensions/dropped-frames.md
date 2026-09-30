---
title: ドロップされたフレーム（寸法）
description: セッションあたりの累積ドロップフレーム数を報告します。
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
source-wordcount: '183'
ht-degree: 7%
---

# ドロップされたフレーム（寸法）

>[!BEGINSHADEBOX]

*このページでは、**削除されたフレーム**&#x200B;のディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.droppedFrameCount` コンテキストデータ変数からペアの[&#x200B; ドロップされたフレーム（指標） &#x200B;](/help/reporting/metrics/dropped-frames.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.droppedFrames` フィールドを公開します。 この変数の収集方法については、[削除されたフレーム &#x200B;](/help/implementation/variables/quality/dropped-frames.md)を参照してください。*

>[!ENDSHADEBOX]

**ドロップされたフレーム** ディメンションは、セッション中にドロップされたフレームの累積数を報告します。 ディメンションを使用して、正確なドロップ数でエンゲージメントを分割します。

## このディメンションの入力方法

ドロップを蓄積すると、プレーヤーはQoE オブジェクトの`droppedFrames`値を更新します。 バックエンドは、クローズコールの最新の値をレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.droppedFrameCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されるリテラルのドロップカウント値です。 セッションレベルのブール値レポートの場合（任意のフレームがドロップされたかどうかにかかわらず）、[&#x200B; ドロップされたフレームの影響を受けるストリーム &#x200B;](/help/reporting/metrics/dropped-frame-impacted-streams.md)を使用します。
