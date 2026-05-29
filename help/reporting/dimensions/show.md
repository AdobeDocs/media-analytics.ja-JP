---
title: 番組
description: シリーズの一部であるビデオコンテンツのプログラム名またはシリーズ名をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# 番組

>[!BEGINSHADEBOX]

*このページでは、**Show**&#x200B;レポートディメンションについて説明します。 この変数の収集方法については、[Show](/help/implementation/variables/standard-metadata/show.md)を参照してください。*

>[!ENDSHADEBOX]

**表示** ディメンションは、プログラムまたはシリーズ名をレポートします。 複数のシーズンのエピソードが同じショーライン項目にロールアップされるため、シリーズの全期間を通じたエンゲージメントを比較するために使用できます。

## このディメンションの入力方法

ショーは、コンテンツがシリーズの一部であるセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.show`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## ディメンション項目

各項目は、セッション開始時に報告されたリテラルの表示名です（例：`"Blinding Light"`）。 1つの単語を共有する無関係なプログラム間でデータが折りたたまれないように、番組ごとに安定した明確な名前を使用します。
