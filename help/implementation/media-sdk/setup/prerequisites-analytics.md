---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装で Streaming Media Collection を使用するための前提条件を説明します
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 44%

---

# Adobe Analytics のみの実装の前提条件

この節で説明する前提条件は、（Edgeを使用していない場合に）Adobeのみの実装を使用した Streaming Media Collection の実装に固有です。

1. **一般的な前提条件を満たす**<br>
Streaming Media Collection をAdobe Analyticsのみの実装用に実装する場合でも、Edge実装の場合でも、[ 一般的な前提条件 ](/help/getting-started/prereqs.md) を満たしていることを確認してください。

1. **Adobe Analyticsが実装されていることを確認する**<br>
Streaming Media Collection を Analytics のみの実装で実装する場合は、Adobe Analyticsの基本的な実装も必要です。 詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーの URL を取得する**<br> メディアトラッキングサーバーの URL については、Adobe Analytics の営業担当または販売店にお問い合わせください。 これは、Mobile SDK、JavaScript SDKおよび Roku の非収集 API トラッキングサーバーの `collection-api-server` URL です。 API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在の Media SDK をダウンロードするか、必要な拡張機能を実装する**<br> 実装パスに応じて、web、モバイルまたは OTT（オーバーザトップ）プラットフォーム用の[最新の SDK をダウンロード](/help/getting-started/download-sdks.md)します。ストリーミングメディアコレクション拡張機能のパスを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。
