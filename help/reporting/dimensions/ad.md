---
title: 広告
description: 広告IDでキーを設定して、再生された各一意の広告をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# 広告

>[!BEGINSHADEBOX]

*このページでは、**Ad**&#x200B;レポートディメンションについて説明します。 この変数の収集方法については、[Ad ID](/help/implementation/variables/ads/ad-id.md)を参照してください。*

>[!ENDSHADEBOX]

**広告** ディメンションは、[広告の開始日](/help/implementation/events/ads/ad-start.md)に設定された広告IDでキーを設定した、各一意の広告が再生されたことをレポートします。 ディメンションは、広告レポートの主要な分類であり、広告名、広告の長さ、Creative IDなどの広告レベルの分類の結合キーです。

## このディメンションの入力方法

広告は、広告の安定した識別子として、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.name`から自動的に収集されます。 訪問の期間を保持します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>Ad IDは必須です。 未設定または空の場合、広告はストリーミングメディア広告レポートからドロップされます。

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告された一意の広告IDです。 クリエイティブごとに安定した識別子を使用することで、セッションをまたいで同じ広告を1行のアイテムまでロールアップできます。
