---
title: ネットワーク
description: ブロードキャストネットワークまたはチャネル名を報告します。
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
source-wordcount: '127'
ht-degree: 12%
---

# ネットワーク

>[!BEGINSHADEBOX]

*このページでは、**ネットワーク**のレポートディメンションについて説明します。 この変数の収集方法については、[ ネットワーク ](/help/implementation/variables/standard-metadata/network.md)を参照してください。*

>[!ENDSHADEBOX]

**ネットワーク** ディメンションは、ブロードキャスト ネットワークまたはチャネル名（例：`"Fox"`または`"ESPN"`）を報告します。 同じストリーミングプロパティ内のネットワーク間のエンゲージメントを比較するために使用します。

## このディメンションの入力方法

ネットワークは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.network`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## ディメンション項目

各項目は、セッション開始時に報告されるリテラルネットワーク値です。 ネットワークごとに安定した明確な名前を使用し、スペルのバリエーション間でデータが断片化しないようにします。
