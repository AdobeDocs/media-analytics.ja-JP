---
title: 作成者
description: コンテンツの作成者にレポートを送信します。 主にオーディオブックに使用されます。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

---


# 作成者

>[!BEGINSHADEBOX]

*このページでは、**作成者**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[作成者](/help/implementation/variables/standard-metadata/author.md)を参照してください。*

>[!ENDSHADEBOX]

**作成者** ディメンションは、コンテンツの作成者をレポートします（例：`"Eleanor Clementine"`）。 主にオーディオブックに使用されますが、ホストまたはプロデューサーが関連するアトリビューションを持つポッドキャストにも有効です。

## このディメンションの入力方法

オーサーは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.author`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラル作成者名です。
