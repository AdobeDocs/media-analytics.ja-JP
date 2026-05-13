---
title: コンテンツタイプ
description: ストリームのフォーマット（VOD、ライブ、リニア、ポッドキャスト、曲など）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%

---


# コンテンツタイプ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツタイプ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツタイプ &#x200B;](/help/implementation/variables/core/content-type.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツタイプ** ディメンションは、ストリームのフォーマットをレポートします（例えば、ビデオの場合はVOD、ライブ、リニア、オーディオの場合はソング、ポッドキャスト、オーディオブック）。

## このディメンションの入力方法

コンテンツタイプは、セッション開始時にプレーヤーによって設定され、すべてのイベントを通して実行されます。 これは派生しません。レポートされた値は、収集中に送信された値と一致します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.contentType`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videocontenttype, post_videocontenttype` |

>[!IMPORTANT]
>
>コンテンツタイプが設定されていないか、空の場合、ディメンションはセッションの`missing_content_type`を報告します。 この値を使用して、修正が必要な実装を検索します。

## ディメンション項目

Adobeで定義された値は、組み込みのセグメントとレポートに入力されます。 カスタム文字列は使用できますが、組み込みセグメントと一致しません。

| ストリームタイプ | 推奨値 |
| --- | --- |
| ビデオ | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Audio | `song`, `podcast`, `audiobook`, `radio` |

## 推奨セグメント

| セグメント | 規則 |
| --- | --- |
| [!UICONTROL VOD コンテンツ &#x200B;] | コンテンツの種類= `vod` |
| [!UICONTROL &#x200B; ライブコンテンツ &#x200B;] | コンテンツの種類= `live` |
| [!UICONTROL 線形コンテンツ &#x200B;] | コンテンツの種類= `linear` |
