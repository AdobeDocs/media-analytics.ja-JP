---
title: 広告
description: 広告IDでキーを設定して、再生された各一意の広告をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 6%

---


# 広告

>[!BEGINSHADEBOX]

*このページでは、**Ad**&#x200B;レポートディメンションについて説明します。 この変数の収集方法については、[Ad ID](/help/implementation/variables/ads/ad-id.md)を参照してください。*

>[!ENDSHADEBOX]

**Ad** ディメンションは、`media.adStart`に設定された広告IDにキーを設定して、再生された各一意の広告をレポートします。 ディメンションは、広告レポートの主要な分類であり、広告名、広告の長さ、Creative IDなどの広告レベルの分類の結合キーです。

## このディメンションの入力方法

広告は、`media.adStart` イベントごとにプレーヤーによって広告の安定した識別子として設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.name`から自動的に収集されます。 訪問の期間を保持します。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoad, post_videoad` |

>[!IMPORTANT]
>
>Ad IDは必須です。 未設定または空の場合、広告はストリーミングメディア広告レポートからドロップされます。

## ディメンション項目

各項目は、`media.adStart`に報告された一意の広告IDです。 クリエイティブごとに安定した識別子を使用することで、セッションをまたいで同じ広告を1行のアイテムまでロールアップできます。
