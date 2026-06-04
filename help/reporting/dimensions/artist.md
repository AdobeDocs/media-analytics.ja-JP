---
title: 作者名
description: オーディオコンテンツのパフォーマンス中のアーティストを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 10%

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
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.artist`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルアーティスト名です。 アーティストごとに安定した正規名を使用することで、書式設定のバリエーション間でデータが断片化しないようにします。
