---
title: コンテンツタイプ
description: ストリームのフォーマット（VOD、ライブ、リニア、ポッドキャスト、曲など）をレポートします。
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
source-wordcount: '210'
ht-degree: 15%
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
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.contentType`から自動的に収集されます。 |
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
| [!UICONTROL VOD コンテンツ &#x200B;] | コンテンツの種類= `vod` |
| [!UICONTROL &#x200B; ライブコンテンツ &#x200B;] | コンテンツの種類= `live` |
| [!UICONTROL 線形コンテンツ &#x200B;] | コンテンツの種類= `linear` |
