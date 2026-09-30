---
title: 発行者
description: 音声コンテンツパブリッシャーを報告します。
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
source-wordcount: '114'
ht-degree: 12%
---

# 発行者

>[!BEGINSHADEBOX]

*このページでは、**発行者**のレポートディメンションについて説明します。 この変数の収集方法については、[Publisher](/help/implementation/variables/standard-metadata/publisher.md)を参照してください。*

>[!ENDSHADEBOX]

**発行者** ディメンションは、音声コンテンツ発行者（ポッドキャストネットワークや音声ブック発行者など）をレポートします。 厳選されたオーディオカタログで、メディア企業間のエンゲージメントを比較するために使用できます。

## このディメンションの入力方法

パブリッシャーは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.publisher`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル媒体体体者名です。
