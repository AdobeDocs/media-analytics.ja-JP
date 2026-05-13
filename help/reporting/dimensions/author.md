---
title: 作成者
description: コンテンツの作成者にレポートを送信します。 主にオーディオブックに使用されます。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 10%

---


# 作成者

>[!BEGINSHADEBOX]

*このページでは、**作成者**のレポートディメンションについて説明します。 この変数の収集方法については、[作成者](/help/implementation/variables/standard-metadata/author.md)を参照してください。*

>[!ENDSHADEBOX]

**作成者** ディメンションは、コンテンツの作成者をレポートします（例：`"Eleanor Clementine"`）。 主にオーディオブックに使用されますが、ホストまたはプロデューサーが関連するアトリビューションを持つポッドキャストにも有効です。

## このディメンションの入力方法

オーサーは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  オーディオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.author`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioauthor` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラル作成者名です。
