---
title: ストリーミングメディア用Chromecastの設定
description: Analyticsのみのストリーミングメディア実装用Chromecast用Media SDKをインストールして設定します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%

---

# ストリーミングメディア用Chromecastの設定

Media SDK for Chromecastは、Chromecast受信者アプリからストリーミングメディアデータをAdobe Analyticsに直接送信します。 SDKとそのドキュメントはGitHubでホストされています。

* **前提条件**:
   * [Analyticsのみの実装の概要](overview.md)を完了します。
   * [Chromecast用Media SDKをダウンロード ](/help/getting-started/download-sdks.md)。

## SDKのインストールと設定

Chromecast受信機アプリにSDKを追加し、正規表現の説明に従ってトラッカーを設定します。

* [Chromecast SDKの設定](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Chromecast SDK API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## メディアイベントの追跡

トラッカーを作成したら、トラッカーのメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[ イベント ](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md) ページの&#x200B;**Chromecast** タブを参照してください。

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [Chromecast SDK API リファレンス ](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [ イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
