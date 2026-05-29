---
title: ステーション
description: オーディオ放送コンテンツのラジオ局名またはIDを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# ステーション

>[!BEGINSHADEBOX]

*このページでは、**Station**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Station](/help/implementation/variables/standard-metadata/station.md)を参照してください。*

>[!ENDSHADEBOX]

**Station** ディメンションは、音声コンテンツを放送するラジオ局名またはID （`"NPR"`または`"WXYZ-FM"`など）を報告します。 このソリューションを使用して、シンジケート ネットワーク内のステーション間のエンゲージメントを比較します。

## このディメンションの入力方法

オーディオコンテンツの場合、セッション開始時にプレーヤーによってステーションが設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.station`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルステーション名またはIDです。 ステーションごとに1つの正規IDを使用して、コールサインのバリエーション間でエンゲージメントが断片化しないようにします。
