---
title: メディアフィードタイプ
description: 同じコンテンツが複数のフィードを介して配信される場合、ブロードキャストフィード（East-HDまたはWest-SDなど）を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# メディアフィードタイプ

>[!BEGINSHADEBOX]

*このページでは、**メディアフィードの種類**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; メディアフィードの種類](/help/implementation/variables/standard-metadata/media-feed-type.md)を参照してください。*

>[!ENDSHADEBOX]

**メディアフィードの種類** ディメンションは、各セッションのブロードキャストフィードをレポートします（例：`"East-HD"`、`"West-SD"`、または`"4K"`）。 複数の地域または品質のフィードを通じて同じコンテンツが配信され、フィードごとにエンゲージメントを報告する必要がある場合に使用します。

## このディメンションの入力方法

メディアフィードの種類は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.feed`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルフィード値です。 地域または品質の分割ごとに、安定したフィード識別子のセットを使用します。
