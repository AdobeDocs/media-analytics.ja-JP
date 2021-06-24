---
title: カスタムメタデータのサポート
description: 「sessionStart、chapterStartおよびadStartイベントでカスタムのキーと値のペアを提供する方法を説明します。」
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 88%

---

# カスタムメタデータのサポート{#custom-metadata-support}

`sessionStart`、`chapterStart` および `adStart` イベントには、カスタムのキーと値のペアを指定できます。この情報は、`customMetadata` キーと共に配置される `params` JSON キーに指定する必要があります。

`customMetadata` JSON キーには、キーと値のペアのオブジェクトを含める必要があります。キーには、英数字、下線、ドットおよびピリオドのみを使用できます。

[MA コレクション API イベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## 例

現在、次のキーと値のペアを使用して `sessionStart` イベントを送信できます。

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

上記の設定では、Analytics に送信されるレポートデータは次のようになります。

`c.a.media.channel=channel-2`

### 推奨

カスタムメタデータには、別個の名前空間を使用することをお勧めします。 次に例を示します。

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

推奨される例では、Analytics に送信されるカスタムメタデータのレポートデータは次のようになります。

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
