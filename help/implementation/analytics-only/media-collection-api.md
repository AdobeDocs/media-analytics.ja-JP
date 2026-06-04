---
title: ストリーミングメディア用のMedia Collection APIの設定
description: Media Collection APIを使用して、RESTful HTTP呼び出しを使用して、ストリーミングメディアデータをAdobe Analyticsに直接送信します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# ストリーミングメディア用のMedia Collection APIの設定

Media Collection APIは、RESTful HTTP呼び出しを使用して、ストリーミングメディアデータをAdobe Analyticsに直接送信します。 完全にカスタマイズ可能なので、SDKでカバーされていないカスタムトラッキングとデバイスをサポートしています。 SDKが選択肢にない場合に使用します。

* **前提条件**: [Analyticsのみの実装の概要](overview.md)を完了します。

## APIの実装

`sessionStart` リクエストを含むセッションを開き、その後に返されるセッションに後続のイベントを送信します。 リクエスト/レスポンスの形式、パラメーター、検証スキーマ、実装ガイダンスについて詳しくは、[Media Collection API リファレンス &#x200B;](../media-collection-api/mc-api-overview.md)を参照してください。

## メディアイベントの追跡

正確なペイロードについては、各[&#x200B; イベント &#x200B;](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md) ページの&#x200B;**メディアコレクション API** タブを参照してください。

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [Media Collection API リファレンス &#x200B;](../media-collection-api/mc-api-overview.md)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
