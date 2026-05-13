---
title: 発行者
description: 音声コンテンツパブリッシャーを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 10%

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
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.publisher`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiopublisher` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル媒体体体者名です。
