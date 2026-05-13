---
title: アルバム
description: オーディオトラックが属するアルバムをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 8%

---


# アルバム

>[!BEGINSHADEBOX]

*このページでは、**アルバム**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Album](/help/implementation/variables/standard-metadata/album.md)を参照してください。*

>[!ENDSHADEBOX]

**アルバム** ディメンションは、オーディオトラックが属するアルバムをレポートします（例：`"Pinegrove"`）。 同じアルバムのトラック間でエンゲージメントをロールアップするために使用します。

## このディメンションの入力方法

アルバムは、オーディオコンテンツのセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; オーディオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.album`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoaudioalbum` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルアルバムタイトルです。 異なるアーティストの同じタイトルを持つ2つのアルバムが1つの行アイテムに折りたたまれます。 [Artist](artist.md) ディメンションと組み合わせて曖昧さを解消します。
