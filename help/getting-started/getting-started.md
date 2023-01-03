---
title: はじめに
description: Adobe Analytics for Streaming Media の基本を学びます。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%

---

# はじめに {#getting-started}

Adobe Analytics for Streaming Media には、Media SDK と Media Collection API の 2 つの主な実装方法があります。

![メソッド](assets/getting-started2.png)

**Media SDK** の組み込みロジックを使用すると、web サイト、携帯電話、コネクテッド TV、タブレット、OTT デバイス、セットトップボックス、ゲームコンソールなど、複数のメディアプラットフォームを正確に測定できます。ダウンロードされたコンテンツも測定できます。 ユーザーに対するエンゲージメントの閲覧に深く関わるインサイトを活用して、閲覧者の関与する期間、日時、場所を把握できます。Media SDK は、**Media Collection API** をトラッキングに使用します。アプリケーションでカスタムトラッキング機能が必要な場合は、Media Collection API をカスタマイズできます。Media SDK でサポートされていないデバイスの場合は、Media Collection API を使用できます。

Adobe Analytics Streaming Media ソリューションは、次のメディアプラットフォームに対して提供されます。

* Web
* モバイル
* OTT（オーバーザトップ）
* ストリーミングメディアやサーバー間の統合に使用できるコネクテッドデバイス

詳しくは、[サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md)を参照してください。

>[!IMPORTANT]
>
>Adobe Analytics Streaming Media を実装するには、アドビ営業担当または販売店に連絡して、Streaming Media が製品ポートフォリオに含まれていることを確認してください。

## Streaming Media 用 Media SDK {#media-sdks}

ストリーミングメディア用 Media SDK は、JavaScript、Android、iOS、tvOS、Chromecast、Roku の各プラットフォームで使用できます。

Media SDK のダウンロードとインストールについて詳しくは、[Media SDK、タグを使用した拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください。


## Media Collection API {#media-collection-apis}

**Media Collection API** を使用すると、メディア分析の実装をカスタマイズできます。Media Collection API を使用してアドビのサーバーを直接呼び出し、SDK などを使用して実行できるほぼすべてのアクションを実行します。データ収集をカスタマイズして、ストリーミングメディアデータに関する重要な質問を調べたり、インサイトを得たり、回答したりするレポートを作成します。

Media Collection API の使用について詳しくは、[Steaming Media API ドキュメント](/help/implementation/media-collection-api/mc-api-overview.md)を参照してください。