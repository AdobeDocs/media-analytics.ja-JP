---
title: ジャンル
description: レポートのコンテンツのジャンル： マルチジャンルのコンテンツは、ライン項目ごとに分割され、それぞれに同じ指標の重みが適用されます。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

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
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、（リスト変数として保存されている）コンテキストデータ `a.media.genre`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting)または[`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) （レガシー） |
| データフィード | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## ディメンション項目

各項目はジャンル値です。 マルチジャンルのセッション （例：`"Drama,Action"`）は、2つの個別の行アイテム （`Drama`と`Action`）として表示され、各アイテムにはセッションの完全なクレジットが割り当てられます。
