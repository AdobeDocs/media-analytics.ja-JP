---
title: ラベル
description: オーディオコンテンツをリリースしたレコードラベルを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# ラベル

>[!BEGINSHADEBOX]

*このページでは、**ラベル**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Label](/help/implementation/variables/standard-metadata/label.md)を参照してください。*

>[!ENDSHADEBOX]

**Label** ディメンションは、オーディオコンテンツをリリースしたレコードラベルをレポートします（例：`"Capitol Records"`）。 音楽またはポッドキャストカタログのラベル間でエンゲージメントを比較するために使用します。

## このディメンションの入力方法

オーディオコンテンツのラベルは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.label`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudiolabel` |

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラルラベル名です。 ラベルごとに安定した正規名を使用することで、スペルやインプリントのバリエーションをまたいでエンゲージメントが断片化するのを防ぎます。
