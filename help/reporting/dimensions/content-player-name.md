---
title: コンテンツプレーヤー名
description: 各メディアセッションをレンダリングしたプレーヤーをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---


# コンテンツプレーヤー名

>[!BEGINSHADEBOX]

*このページでは、**コンテンツプレーヤー名**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツプレーヤー名](/help/implementation/variables/core/content-player-name.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツプレーヤー名** ディメンションは、各メディアセッションをレンダリングしたプレーヤー（`HTML5 Player`、`Brightcove`、または`Roku Player`など）をレポートします。 同じプロパティのプレーヤー間のエンゲージメント、完了率、品質を比較するために使用します。

## このディメンションの入力方法

プレーヤー名は、セッション開始時にプレーヤーによって設定され、セッションの期間にわたって保持されます。 値は、すべてのイベントで送信され、Adobe AnalyticsとCustomer Journey Analyticsの両方でレポートされます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.playerName`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>プレーヤー名が設定されていない場合、ディメンションはそのセッションに入力されません。 プレーヤー名のないセッションは、レポートでプレーヤーごとに分割できません。

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル文字列です。 プレーヤーごとに安定した明確な名前を使用して、異なるプレーヤーのデータが1つの行のアイテムに折りたたまれないようにします。
