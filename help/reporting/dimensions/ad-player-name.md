---
title: 広告プレーヤー名
description: 各広告をレンダリングしたプレーヤーをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# 広告プレーヤー名

>[!BEGINSHADEBOX]

*このページでは、**広告プレーヤー名**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Ad player name](/help/implementation/variables/ads/ad-player-name.md)を参照してください。*

>[!ENDSHADEBOX]

**広告プレーヤー名** ディメンションは、各広告をレンダリングしたプレーヤーをレポートします（例：`"Freewheel"`、`"Google IMA"`）。 広告プレーヤは、サーバサイドの広告挿入サービスによって広告がステッチされる場合、メインコンテンツプレーヤとは異なっていてもよい。

## このディメンションの入力方法

広告プレーヤー名は、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.playerName`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル広告プレーヤー名です。
