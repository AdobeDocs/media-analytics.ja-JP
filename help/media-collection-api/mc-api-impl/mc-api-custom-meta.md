---
title: カスタムメタデータのサポート
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# カスタムメタデータのサポート{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

The `customMetadata` JSON key should contain an object of key:value pairs. キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MAコレクションAPIイベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

