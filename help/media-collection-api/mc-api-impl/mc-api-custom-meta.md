---
title: カスタムメタデータのサポート
description: カスタムメタデータのサポート
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# カスタムメタデータのサポート {#custom-metadata-support}

`sessionStart`、`chapterStart` および `adStart` イベントには、カスタムのキーと値のペアを指定できます。この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

`customMetadata` JSON キーには、キーと値のペアのオブジェクトを含める必要があります。キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MA コレクション API イベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
