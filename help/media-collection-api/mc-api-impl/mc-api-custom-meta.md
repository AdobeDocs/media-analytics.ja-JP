---
seo-title: カスタムメタデータのサポート
title: カスタムメタデータのサポート
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# カスタムメタデータのサポート{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

The `customMetadata` JSON key should contain an object of key:value pairs. キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MAコレクションAPIイベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

