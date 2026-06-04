---
title: 発行者
description: 音声コンテンツパブリッシャーを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 発行者

>[!BEGINSHADEBOX]

*このページでは、**発行者**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Publisher](/help/implementation/variables/standard-metadata/publisher.md)を参照してください。*

>[!ENDSHADEBOX]

**発行者** ディメンションは、音声コンテンツ発行者（ポッドキャストネットワークや音声ブック発行者など）をレポートします。 厳選されたオーディオカタログで、メディア企業間のエンゲージメントを比較するために使用できます。

## このディメンションの入力方法

パブリッシャーは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.publisher`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル媒体体体者名です。
