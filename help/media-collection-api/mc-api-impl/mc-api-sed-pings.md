---
title: ping イベントの送信
description: ping イベントの送信
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '88'
ht-degree: 100%

---

# ping イベントの送信 {#sending-ping-events}

**メインコンテンツに対しては、他にどのような API イベントが送信されているかに関係なく、再生を開始した 10 秒後から 10 秒ごとに ping イベントを発生させる必要があります。広告トラッキングの場合、1 秒ごとに ping イベントを発生させる必要があります。**

ping イベントは、文字どおり Media Analytics の「ハートビート」です。ping 呼び出しの必須パラメーターは、`eventType: ping` と `playerTime` オブジェクトのみです（再生ヘッドの位置とタイムスタンプ）。

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
