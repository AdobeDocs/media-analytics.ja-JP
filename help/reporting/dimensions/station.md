---
title: ステーション
description: オーディオ放送コンテンツのラジオ局名またはIDを報告します。
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
source-wordcount: '138'
ht-degree: 10%
---

# ステーション

>[!BEGINSHADEBOX]

*このページでは、**Station**のレポートディメンションについて説明します。 この変数の収集方法については、[Station](/help/implementation/variables/standard-metadata/station.md)を参照してください。*

>[!ENDSHADEBOX]

**Station** ディメンションは、音声コンテンツを放送するラジオ局名またはID （`"NPR"`または`"WXYZ-FM"`など）を報告します。 このソリューションを使用して、シンジケート ネットワーク内のステーション間のエンゲージメントを比較します。

## このディメンションの入力方法

オーディオコンテンツの場合、セッション開始時にプレーヤーによってステーションが設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.station`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルステーション名またはIDです。 ステーションごとに1つの正規IDを使用して、コールサインのバリエーション間でエンゲージメントが断片化しないようにします。
