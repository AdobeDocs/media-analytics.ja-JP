---
title: 広告ロード数
description: 各ストリーミングメディアセッションに使用される広告ロードのタイプをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# 広告ロード数

>[!BEGINSHADEBOX]

*このページでは、**広告が**&#x200B;件のレポート ディメンションを読み込みます。 この変数の収集方法については、[Ad load type](/help/implementation/variables/standard-metadata/ad-load-type.md)を参照してください。*

>[!ENDSHADEBOX]

「**広告が読み込まれる**」ディメンションは、各ストリーミングメディアセッションの開始時に読み込まれた広告のタイプをレポートします。 値は顧客が定義しているため、組織は広告配信メカニズム（`"linear"`、`"dynamic"`、または`"programmatic"`など）でセッションを分類できます。

## このディメンションの入力方法

広告の読み込みタイプは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ストリーミングメディア &#x200B;]](/help/reporting/setup/analytics-reporting.md)が設定されている場合、コンテキストデータ `a.media.adLoad`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル広告ロードタイプの文字列です。 値は標準的な列挙に制約されません。実装全体で一貫性のある分類法を定義することで、値がレポートで予測可能にロールアップされます。
