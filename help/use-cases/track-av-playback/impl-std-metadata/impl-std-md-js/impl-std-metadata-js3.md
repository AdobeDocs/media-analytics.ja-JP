---
title: JavaScript 3.x を使用した標準メタデータの実装
description: ブラウザーアプリ（JS 3.x）で標準ビデオメタデータや標準広告メタデータをトラッキングコールで送信するように設定する方法を説明します。
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 100%

---

# JavaScript 3.x を使用した標準メタデータの実装 {#implement-standard-metadata-on-javascript}

## 実装

コンテキストデータオブジェクトをインスタンス化し、必要な標準メタデータ変数に値を設定します。 次に例を示します。

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
