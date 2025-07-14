---
title: ping イベントの送信
description: ping イベントは、Streaming Media コレクションのハートビートです。 メインコンテンツまたは広告トラッキング用の時間指定 ping を送信する方法を説明します。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 51%

---

# ping イベントの送信{#sending-ping-events}

**送信した他の API イベントに関係なく、再生から 10 秒後に 10 秒ごとに ping イベントを発生させる必要があります。 これは、メインコンテンツと広告トラッキングの両方に適用されます。**

ping イベントは、Streaming Media コレクションの「ハートビート」です。 ping 呼び出しの必須パラメーターは、`eventType: ping` と `playerTime` オブジェクトのみです（再生ヘッドの位置とタイムスタンプ）。

次のコードスニペットは、メインコンテンツの時間指定された ping メカニズム（10 秒間隔）を実装する 1 つの方法を示しています。

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
