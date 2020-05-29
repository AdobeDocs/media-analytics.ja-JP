---
title: JavaScript 3.xを使用した標準メタデータの実装
description: ブラウザーアプリ（JS）上で、標準ビデオおよび広告メタデータがトラッキングコールで送信されるようにする設定を説明します。
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# JavaScript 3.xを使用した標準メタデータの実装{#implement-standard-metadata-on-javascript}

## 実装

コンテキストデータオブジェクトをインスタンス化し、必要な標準メタデータ変数を設定します。 次に例を示します。

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
