---
title: 作者名
description: オーディオコンテンツのパフォーマンス中のアーティストを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# 作者名

>[!BEGINSHADEBOX]

*このページでは、**アーティスト**のレポートディメンションについて説明します。 この変数の収集方法については、[Artist](/help/implementation/variables/standard-metadata/artist.md)を参照してください。*

>[!ENDSHADEBOX]

**Artist** ディメンションは、オーディオコンテンツに対するパフォーマンスの高いアーティストをレポートします（例：`"Crested Larks"`）。 これを使用すると、音楽やポッドキャストのカタログに対するエンゲージメントをパフォーマーごとに分割できます。

## このディメンションの入力方法

アーティストは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.artist`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioartist` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルアーティスト名です。 アーティストごとに安定した正規名を使用することで、書式設定のバリエーション間でデータが断片化しないようにします。
