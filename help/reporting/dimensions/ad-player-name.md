---
title: 広告プレーヤー名
description: 各広告をレンダリングしたプレーヤーをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# 広告プレーヤー名

>[!BEGINSHADEBOX]

*このページでは、**広告プレーヤー名**のレポートディメンションについて説明します。 この変数の収集方法については、[Ad player name](/help/implementation/variables/ads/ad-player-name.md)を参照してください。*

>[!ENDSHADEBOX]

**広告プレーヤー名** ディメンションは、各広告をレンダリングしたプレーヤーをレポートします（例：`"Freewheel"`、`"Google IMA"`）。 広告プレーヤは、サーバサイドの広告挿入サービスによって広告がステッチされる場合、メインコンテンツプレーヤとは異なっていてもよい。

## このディメンションの入力方法

広告プレーヤー名は、プレーヤーが`media.adStart` イベントごとに設定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.playerName`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadplayername, post_videoadplayername` |

## ディメンション項目

各項目は、`media.adStart`に報告されたリテラル広告プレーヤー名です。
