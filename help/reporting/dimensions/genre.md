---
title: ジャンル
description: レポートのコンテンツのジャンル： マルチジャンルのコンテンツは、ライン項目ごとに分割され、それぞれに同じ指標の重みが適用されます。
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
source-wordcount: '181'
ht-degree: 8%
---

# ジャンル

>[!BEGINSHADEBOX]

*このページでは、**ジャンル**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; ジャンル &#x200B;](/help/implementation/variables/standard-metadata/genre.md)を参照してください。*

>[!ENDSHADEBOX]

**ジャンル** ディメンションは、コンテンツのジャンルをレポートします。 ジャンルは、コンマ区切りの文字列として収集され、リストディメンションとして保存されます。 マルチジャンルのコンテンツは、別々のラインアイテムに分割され、それぞれに同じ指標の重みが適用されます。 このソリューションを利用すれば、単一のマルチジャンルのアセットに費やした時間を二重計上することなく、ジャンルをまたいでエンゲージメントを比較できます。

## このディメンションの入力方法

ジャンルはセッション開始時にプレイヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、（リスト変数として保存されている）コンテキストデータ `a.media.genre`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting)または[`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) （レガシー） |
| データフィード | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## ディメンション項目

各項目はジャンル値です。 マルチジャンルのセッション （例：`"Drama,Action"`）は、2つの個別の行アイテム （`Drama`と`Action`）として表示され、各アイテムにはセッションの完全なクレジットが割り当てられます。
