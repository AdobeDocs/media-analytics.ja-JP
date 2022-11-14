---
title: Adobe Analytics用ストリーミングメディアの実装
description: ストリーミングメディアの実装パスについて説明します。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Adobe Analytics用ストリーミングメディアの実装

従う実装パスは、メディア SDK の組み込みロジック（標準、推奨される実装）を使用するか、独自にロールしてシンプルで強力でカスタマイズ可能なメディアコレクション API(RESTful) を使用するかによって異なります。

サポートされているプラットフォームに応じて実装パスを選択します。 一部のプレーヤーは、メディア SDK またはAdobe Experience Platform Media SDK でサポートされていません。メディアコレクション API は、これらのプレーヤーをサポートする方法を提供します。 サポートされるデバイスについて詳しくは、 [サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md).

![メディアフロー](media-sdk/assets/choose-media-flow2.png)

メディア SDK と拡張機能のダウンロードとインストールについて詳しくは、 [タグを使用したメディア SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md).

メディアコレクション API の使用について詳しくは、 [メディアコレクション API](media-collection-api/mc-api-overview.md).
