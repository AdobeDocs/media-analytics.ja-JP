---
title: メディアのダウンロード
description: ダウンロードされたオフラインコンテンツを再生したセッションをフラグします。
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
source-wordcount: '195'
ht-degree: 7%
---

# メディアのダウンロード

>[!BEGINSHADEBOX]

*このページでは、**メディアのダウンロード**レポート ディメンションについて説明します。 この変数の収集方法については、[ メディアがダウンロードしたフラグ ](/help/implementation/variables/core/media-downloaded-flag.md)を参照してください。*

>[!ENDSHADEBOX]

**メディアがダウンロードした** ディメンションは、インターネットからのライブストリームではなく、以前にダウンロードしたオフラインコンテンツを再生したセッションにフラグを付けます。 エンゲージメント、完了率、品質を比較する際に、オフライン再生とストリーミングセッションを分離するために使用できます。

## このディメンションの入力方法

ダウンロードされたフラグは、プレーヤーによって3つの方法のいずれかで設定されます。 フラグを使用してトラッカーを初期化する（Mobile SDK）、`sessionStart`を`/downloaded` エンドポイントバリアントに送信する（Media Edge API ダイレクト）、または`sessionStart` パラメーターに`media.downloaded: true`を含める（Media Collection API）。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.downloaded`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.downloaded`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## ディメンション項目

| 値 | 説明 |
| --- | --- |
| `true` | ダウンロードされたオフラインコンテンツが再生されました。 |
| （empty） | そのセッションは生中継された。 フィールドは、`false`に設定するのではなく省略されます。 |
