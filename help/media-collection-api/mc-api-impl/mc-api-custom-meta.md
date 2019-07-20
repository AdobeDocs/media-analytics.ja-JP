---
seo-title: カスタムメタデータのサポート
title: カスタムメタデータのサポート
uuid: df4109dd-9fca-4c33- a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# カスタムメタデータのサポート{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

`customMetadata` JSONキーには、キーのオブジェクトを含める必要があります。valueペアを使用します。キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MAコレクションAPIイベント](../mc-api-ref/mc-api-events-req.md)

