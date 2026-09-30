---
title: 番組
description: シリーズの一部であるビデオコンテンツのプログラム名またはシリーズ名をレポートします。
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
source-wordcount: '158'
ht-degree: 10%
---

# 番組

>[!BEGINSHADEBOX]

*このページでは、**Show**レポートディメンションについて説明します。 この変数の収集方法については、[Show](/help/implementation/variables/standard-metadata/show.md)を参照してください。*

>[!ENDSHADEBOX]

**表示** ディメンションは、プログラムまたはシリーズ名をレポートします。 複数のシーズンのエピソードが同じショーライン項目にロールアップされるため、シリーズの全期間を通じたエンゲージメントを比較するために使用できます。

## このディメンションの入力方法

ショーは、コンテンツがシリーズの一部であるセッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.show`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## ディメンション項目

各項目は、セッション開始時に報告されたリテラルの表示名です（例：`"Blinding Light"`）。 1つの単語を共有する無関係なプログラム間でデータが折りたたまれないように、番組ごとに安定した明確な名前を使用します。
