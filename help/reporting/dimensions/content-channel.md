---
title: コンテンツチャネル
description: 各セッションが再生された配布ステーション、ネットワーク、またはプロパティを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

---


# コンテンツチャネル

>[!BEGINSHADEBOX]

*このページでは、**コンテンツチャネル**のレポートディメンションについて説明します。 この変数の収集方法については、[ コンテンツチャネル ](/help/implementation/variables/core/content-channel.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツチャネル** ディメンションは、各セッションが再生された配布ステーション、ネットワーク、またはプロパティをレポートします。 ネットワークまたはプロパティのセクションごとに再生を分割する場合に使用します。

## このディメンションの入力方法

チャネルは、セッション開始時にプレーヤーによって設定され、セッションの期間にわたって保持されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.channel`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>チャネルが設定されていない場合、ディメンションはそのセッションに対して未入力になります。

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル文字列です。 任意の文字列を使用できます。 一般的な値は、ネットワーク名、サイトパスの一部、または内部プロパティ識別子です。
