---
title: カスタムメタデータのサポート
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# カスタムメタデータのサポート {#custom-metadata-support}

`sessionStart`、`chapterStart` および `adStart` イベントには、カスタムのキーと値のペアを指定できます。この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

`customMetadata` JSON キーには、キーと値のペアのオブジェクトを含める必要があります。キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MA コレクション API イベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

