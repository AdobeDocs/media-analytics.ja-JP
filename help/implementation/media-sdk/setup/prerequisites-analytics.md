---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装で Streaming Media Collection アドオンを使用するための前提条件を説明します
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# Adobe Analytics のみの実装の前提条件

この節で説明する前提条件は、（Edgeを使用しない場合に）Adobe分析専用の実装を使用したストリーミングメディアコレクションアドオンの実装に固有です。

1. **一般的な前提条件を満たす**<br>
Streaming Media Collection アドオンをAdobe Analyticsのみの実装に実装する場合でも、Edgeの実装に実装する場合でも、を満たしていることを確認してください [一般的な前提条件](/help/getting-started/prereqs.md).

1. **Adobe Analyticsが実装されていることを確認します**<br>
Streaming Media Collection アドオンを Analytics のみの実装で実装する場合は、Adobe Analyticsの基本的な実装も必要です。 詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーの URL を取得する**<br> メディアトラッキングサーバーの URL については、Adobe Analytics の営業担当または販売店にお問い合わせください。 これはです `collection-api-server` URL は、Mobile SDK 用、JavaScript SDK 用および Roku の非収集 API トラッキングサーバー用です。 API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在の Media SDK をダウンロードするか、必要な拡張機能を実装する**<br> 実装パスに応じて、web、モバイルまたは OTT（オーバーザトップ）プラットフォーム用の[最新の SDK をダウンロード](/help/getting-started/download-sdks.md)します。ストリーミングメディアコレクションアドオンの拡張機能パスを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。
