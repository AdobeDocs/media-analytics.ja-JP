---
title: 作者名
description: オーディオコンテンツのパフォーマンス中のアーティストを報告します。
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
source-wordcount: '128'
ht-degree: 10%
---

# 作者名

>[!BEGINSHADEBOX]

*このページでは、**アーティスト**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Artist](/help/implementation/variables/standard-metadata/artist.md)を参照してください。*

>[!ENDSHADEBOX]

**Artist** ディメンションは、オーディオコンテンツに対するパフォーマンスの高いアーティストをレポートします（例：`"Crested Larks"`）。 これを使用すると、音楽やポッドキャストのカタログに対するエンゲージメントをパフォーマーごとに分割できます。

## このディメンションの入力方法

アーティストは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.artist`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルアーティスト名です。 アーティストごとに安定した正規名を使用することで、書式設定のバリエーション間でデータが断片化しないようにします。
