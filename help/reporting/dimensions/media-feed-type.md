---
title: メディアフィードタイプ
description: 同じコンテンツが複数のフィードを介して配信される場合、ブロードキャストフィード（East-HDまたはWest-SDなど）を報告します。
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
source-wordcount: '159'
ht-degree: 8%
---

# メディアフィードタイプ

>[!BEGINSHADEBOX]

*このページでは、**メディアフィードの種類**のレポートディメンションについて説明します。 この変数の収集方法については、[ メディアフィードの種類](/help/implementation/variables/standard-metadata/media-feed-type.md)を参照してください。*

>[!ENDSHADEBOX]

**メディアフィードの種類** ディメンションは、各セッションのブロードキャストフィードをレポートします（例：`"East-HD"`、`"West-SD"`、または`"4K"`）。 複数の地域または品質のフィードを通じて同じコンテンツが配信され、フィードごとにエンゲージメントを報告する必要がある場合に使用します。

## このディメンションの入力方法

メディアフィードの種類は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.feed`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルフィード値です。 地域または品質の分割ごとに、安定したフィード識別子のセットを使用します。
