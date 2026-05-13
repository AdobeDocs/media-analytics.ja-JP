---
title: ポッド位置での広告
description: 親の広告ブレーク内の各広告のインデックスが0個の位置をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 6%

---


# ポッド位置での広告

>[!BEGINSHADEBOX]

*このページでは、ポッド位置&#x200B;**の**広告のレポートディメンションについて説明します。 この変数の収集方法については、[ ポッド位置の広告](/help/implementation/variables/ads/ad-in-pod-position.md)を参照してください。*

>[!ENDSHADEBOX]

ポッド位置&#x200B;**の**&#x200B;広告ディメンションは、親の広告枠の中の各広告のインデックスが0個の位置を報告します。 ポッドの最初の広告は`0`、2番目の広告は`1`などです。 ディメンションを使用して、広告枠の中の位置ごとにエンゲージメントと完了率を比較します。

## このディメンションの入力方法

ポッドの位置の広告は、プレーヤーが`media.adStart` イベントごとに設定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.podPosition`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadinpod, post_videoadinpod` |

## ディメンション項目

各項目は整数の位置の値（`0`、`1`、`2`、...）です。 `media.adStart`に報告されました。
