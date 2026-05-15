---
title: シーズン
description: エピソードのコンテンツのシーズン番号を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# シーズン

>[!BEGINSHADEBOX]

*このページでは、**シーズン**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; シーズン &#x200B;](/help/implementation/variables/standard-metadata/season.md)を参照してください。*

>[!ENDSHADEBOX]

**シーズン** ディメンションは、エピソードのコンテンツのシーズン番号をレポートします。 完全なエピソードのブレークアウトには、[Show](show.md)および[Episode](episode.md)と一緒に使用します。

## このディメンションの入力方法

シーズンは、コンテンツがシリーズの一部であるセッション開始時に、プレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.season`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## ディメンション項目

各項目は、セッション開始時に報告されるリテラルシーズン値です（通常は`"1"`、`"2"`などの文字列整数）。 同じ番組のエピソード間で一貫性を持たせます。ディメンションは`"1"`と`"01"`を同じ行項目に正規化しません。
