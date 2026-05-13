---
title: ping イベントの送信
description: Ping イベントは、Adobeのストリーミングメディアサービスの中核です。 メインコンテンツまたは広告トラッキング用の時間指定 ping を送信する方法を説明します。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6R7DILB56bcHgAki-Lvto3yYbuhf-wYfklvPElDeM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 110
ht-degree: 50%

---

# ping イベントの送信{#sending-ping-events}

**送信した他のAPI イベントに関係なく、再生を10秒後から開始して、10秒ごとにping イベントを起動する必要があります。 これは、メインコンテンツと広告トラッキングの両方に適用されます。**

ping イベントは、Adobe ストリーミングメディアサービスの「ハートビート」です。 ping 呼び出しの必須パラメーターは、`eventType: ping` と `playerTime` オブジェクトのみです（再生ヘッドの位置とタイムスタンプ）。

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
