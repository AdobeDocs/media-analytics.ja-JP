---
title: コンテンツタイプ
description: ストリームのフォーマット（VOD、ライブ、リニア、ポッドキャスト、曲など）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# コンテンツタイプ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツタイプ**のレポートディメンションについて説明します。 この変数の収集方法については、[ コンテンツタイプ ](/help/implementation/variables/core/content-type.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツタイプ** ディメンションは、ストリームのフォーマットをレポートします（例えば、ビデオの場合はVOD、ライブ、リニア、オーディオの場合はソング、ポッドキャスト、オーディオブック）。

## このディメンションの入力方法

コンテンツタイプは、セッション開始時にプレーヤーによって設定され、すべてのイベントを通して実行されます。 これは派生しません。レポートされた値は、収集中に送信された値と一致します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.contentType`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

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
| [!UICONTROL VOD コンテンツ ] | コンテンツの種類= `vod` |
| [!UICONTROL  ライブコンテンツ ] | コンテンツの種類= `live` |
| [!UICONTROL 線形コンテンツ ] | コンテンツの種類= `linear` |
