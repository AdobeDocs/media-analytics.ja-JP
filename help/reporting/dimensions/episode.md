---
title: エピソード
description: シーズン内のエピソード番号を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---


# エピソード

>[!BEGINSHADEBOX]

*このページでは、**エピソード**のレポートディメンションについて説明します。 この変数の収集方法については、[ エピソード ](/help/implementation/variables/standard-metadata/episode.md)を参照してください。*

>[!ENDSHADEBOX]

**エピソード** ディメンションは、シーズン内のエピソード番号をレポートします。 [Show](show.md)および[Season](season.md)と一緒に使用すると、個々のエピソード レベルでエンゲージメントを分割できます。

## このディメンションの入力方法

エピソードはセッション開始時にプレイヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.episode`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルエピソード値（通常は`"13"`などの文字列整数）です。 エピソード数だけでは、シーズン全体で一意ではありません。シーズンと組み合わせて、明確なブレイクアウトを行います。
