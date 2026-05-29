---
title: クリエイティブ URL
description: 各広告クリエイティブのアセット URLをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# クリエイティブ URL

>[!BEGINSHADEBOX]

*このページでは、**Creative URL**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Creative URL](/help/implementation/variables/ads/creative-url.md)を参照してください。*

>[!ENDSHADEBOX]

**Creative URL** ディメンションは、各広告クリエイティブのアセット URLをレポートします。 URL自体が分析にとって意味がある場合（CDN パスやクリエイティブバージョンの区別など）は、ディメンションを使用します。

## このディメンションの入力方法

CreativeのURLは、[ad start](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.ad.creativeURL`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.creativeURL`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル URL文字列です。
