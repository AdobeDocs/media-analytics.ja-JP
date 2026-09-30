---
title: 広告ロード数
description: 各ストリーミングメディアセッションに使用される広告ロードのタイプをレポートします。
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
source-wordcount: '161'
ht-degree: 8%
---

# 広告ロード数

>[!BEGINSHADEBOX]

*このページでは、**広告が**件のレポート ディメンションを読み込みます。 この変数の収集方法については、[Ad load type](/help/implementation/variables/standard-metadata/ad-load-type.md)を参照してください。*

>[!ENDSHADEBOX]

「**広告が読み込まれる**」ディメンションは、各ストリーミングメディアセッションの開始時に読み込まれた広告のタイプをレポートします。 値は顧客が定義しているため、組織は広告配信メカニズム（`"linear"`、`"dynamic"`、または`"programmatic"`など）でセッションを分類できます。

## このディメンションの入力方法

広告の読み込みタイプは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ストリーミングメディア ]](/help/reporting/setup/analytics-reporting.md)が設定されている場合、コンテキストデータ `a.media.adLoad`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル広告ロードタイプの文字列です。 値は標準の列挙に制限されません。 実装全体で一貫性のある分類法を定義して、レポートで予測可能に値がロールアップされるようにします。
