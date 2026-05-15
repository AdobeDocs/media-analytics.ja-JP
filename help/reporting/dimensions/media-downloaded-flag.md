---
title: メディアのダウンロード
description: ダウンロードされたオフラインコンテンツを再生したセッションをフラグします。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# メディアのダウンロード

>[!BEGINSHADEBOX]

*このページでは、**メディアのダウンロード**&#x200B;レポート ディメンションについて説明します。 この変数の収集方法については、[&#x200B; メディアがダウンロードしたフラグ &#x200B;](/help/implementation/variables/core/media-downloaded-flag.md)を参照してください。*

>[!ENDSHADEBOX]

**メディアがダウンロードした** ディメンションは、インターネットからのライブストリームではなく、以前にダウンロードしたオフラインコンテンツを再生したセッションにフラグを付けます。 エンゲージメント、完了率、品質を比較する際に、オフライン再生とストリーミングセッションを分離するために使用できます。

## このディメンションの入力方法

ダウンロードされたフラグは、プレーヤーによって3つの方法のいずれかで設定されます。 フラグを使用してトラッカーを初期化する（Mobile SDK）、`sessionStart`を`/downloaded` エンドポイントバリアントに送信する（Media Edge API ダイレクト）、または`sessionStart` パラメーターに`media.downloaded: true`を含める（Media Collection API）。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.downloaded`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.downloaded`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## ディメンション項目

| 値 | 説明 |
| --- | --- |
| `true` | ダウンロードされたオフラインコンテンツが再生されました。 |
| （empty） | そのセッションは生中継された。 フィールドは、`false`に設定するのではなく省略されます。 |
