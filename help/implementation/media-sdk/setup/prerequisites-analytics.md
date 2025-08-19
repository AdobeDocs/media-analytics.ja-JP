---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装に Adobe Analytics for Streaming Media アドオンを使用するための前提条件について説明します
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 43%

---

# Adobe Analytics のみの実装の前提条件

この節で説明する前提条件は、（Edgeを使用していない場合に）Adobe分析専用の実装用の Adobe Analytics for Streaming Media アドオンを実装する場合に固有です。

1. **一般的な前提条件を満たす**<br>
ストリーミングメディアサービスをAdobe Analyticsのみの実装用に実装する場合でも、Edgeの実装用に実装する場合でも、[ 一般的な前提条件 ](/help/getting-started/prereqs.md) を満たしていることを確認してください。

1. **Adobe Analyticsが実装されていることを確認する**<br>
Analytics のみの実装に Adobe Analytics for Streaming Media アドオンを実装する場合は、Adobe Analyticsの基本的な実装も必要です。 詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーの URL を取得する**<br> メディアトラッキングサーバーの URL については、Adobe Analytics の営業担当または販売店にお問い合わせください。 これは、Mobile SDK、JavaScript SDKおよび Roku の非収集 API トラッキングサーバーの `collection-api-server` URL です。 API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在の Media SDK をダウンロードするか、必要な拡張機能を実装する**<br> 実装パスに応じて、web、モバイルまたは OTT（オーバーザトップ）プラットフォーム用の[最新の SDK をダウンロード](/help/getting-started/download-sdks.md)します。Adobe Analytics for Streaming Media アドオンを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。
