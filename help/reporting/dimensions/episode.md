---
title: エピソード
description: シーズン内のエピソード番号を報告します。
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
source-wordcount: '132'
ht-degree: 12%
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
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.episode`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルエピソード値（通常は`"13"`などの文字列整数）です。 エピソード数だけでは、シーズン全体で一意ではありません。シーズンと組み合わせて、明確なブレイクアウトを行います。
