---
title: コンテンツ名
description: 各メディアセッションの人間が判読可能なタイトルをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 8%

---


# コンテンツ名

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ名**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツ名](/help/implementation/variables/core/content-name.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ名** ディメンションは、各メディアセッションの人間が読み取れるタイトルをレポートします。

## このディメンションの入力方法

フレンドリー名は、セッション開始時にプレーヤーによって設定されます。 報告された値は送信された値と一致します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.friendlyName`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoname, post_videoname` |

>[!NOTE]
>
>Adobe Analyticsでは、この値は[&#x200B; コンテンツ &#x200B;](content.md) ディメンションの&#x200B;**ビデオ名**&#x200B;分類にも対応します。 お客様は、その分類を個別に入力および管理する責任があります。 Customer Journey Analyticsは、このディメンションを直接使用します。

>[!IMPORTANT]
>
>コンテンツ名が設定されていない場合、ディメンションはそのセッションに入力されません。

## ディメンション項目

各項目は、セッション開始時に報告されるリテラル タイトルです（例：`"Blinding Light"`）。
