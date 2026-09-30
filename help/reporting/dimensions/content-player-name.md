---
title: コンテンツプレーヤー名
description: 各メディアセッションをレンダリングしたプレーヤーをレポートします。
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
source-wordcount: '196'
ht-degree: 7%
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
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.playerName`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>プレーヤー名が設定されていない場合、ディメンションはそのセッションに入力されません。 プレーヤー名のないセッションは、レポートでプレーヤーごとに分割できません。

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル文字列です。 プレーヤーごとに安定した明確な名前を使用して、異なるプレーヤーのデータが1つの行のアイテムに折りたたまれないようにします。
