---
title: ドロップされたフレーム（寸法）
description: セッションあたりの累積ドロップフレーム数を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---


# ドロップされたフレーム（寸法）

>[!BEGINSHADEBOX]

*このページでは、**削除されたフレーム**&#x200B;のディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.droppedFrameCount` コンテキストデータ変数からペアの[&#x200B; ドロップされたフレーム（指標） &#x200B;](/help/reporting/metrics/dropped-frames.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.droppedFrames` フィールドを公開します。 この変数の収集方法については、[削除されたフレーム &#x200B;](/help/implementation/variables/quality/dropped-frames.md)を参照してください。*

>[!ENDSHADEBOX]

**ドロップされたフレーム** ディメンションは、セッション中にドロップされたフレームの累積数を報告します。 ディメンションを使用して、正確なドロップ数でエンゲージメントを分割します。

## このディメンションの入力方法

ドロップを蓄積すると、プレーヤーはQoE オブジェクトの`droppedFrames`値を更新します。 バックエンドは、クローズコールの最新の値をレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.droppedFrameCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoedroppedframecountevar, post_videoqoedroppedframecountevar` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されるリテラルのドロップカウント値です。 セッションレベルのブール値レポートの場合（任意のフレームがドロップされたかどうかにかかわらず）、[&#x200B; ドロップされたフレームの影響を受けるストリーム &#x200B;](/help/reporting/metrics/dropped-frame-impacted-streams.md)を使用します。
