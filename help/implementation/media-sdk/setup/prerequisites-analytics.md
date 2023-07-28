---
title: Adobe Analyticsのみの実装の前提条件
description: Adobe Analyticsのみの実装でストリーミングメディアを使用するための前提条件について説明します。
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Adobe Analyticsのみの実装の前提条件

この節で説明する前提条件は、Adobe分析のみの実装でのストリーミングメディアの実装（Edge を使用しない場合）に特有です。

1. **一般的な前提条件の完了**<br>
ストリーミングメディアをAdobe Analyticsのみの実装に実装する場合も、Edge の実装に実装する場合も、 [一般的な前提条件](/help/getting-started/prereqs.md).

1. **Adobe Analyticsの実装を確認する**<br>
Analytics のみの実装でストリーミングメディアを実装する場合は、Adobe Analyticsの基本的な実装も必要です。 詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーの URL を取得する**<br> メディアトラッキングサーバーの URL については、Adobe Analytics の営業担当または販売店にお問い合わせください。 この`collection-api-server` URL は、Mobile SDK 用、JavaScript SDK 用および Roku の非収集 APIトラッキングサーバー用です。API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在の Media SDK をダウンロードするか、必要な拡張機能を実装する**<br> 実装パスに応じて、web、モバイルまたは OTT（オーバーザトップ）プラットフォーム用の[最新の SDK をダウンロード](/help/getting-started/download-sdks.md)します。ストリーミングメディア用 Adobe Analytics 拡張機能のパスを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。
