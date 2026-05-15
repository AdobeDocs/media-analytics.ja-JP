---
title: ネットワーク
description: ブロードキャストネットワークまたはチャネル名を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 11%

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
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.network`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## ディメンション項目

各項目は、セッション開始時に報告されるリテラルネットワーク値です。 ネットワークごとに安定した明確な名前を使用し、スペルのバリエーション間でデータが断片化しないようにします。
