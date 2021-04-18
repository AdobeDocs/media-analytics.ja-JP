---
title: イベントの順序の制御
description: イベントの順序の制御
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# イベントの順序の制御 {#controlling-the-order-of-events}

メディアコレクション API は RESTful で、ビデオトラッキングは大きく時間に依存する操作なので、誤った順序でバックエンドに届くメディアコレクション API トラッキングコールが実装者の懸念材料になることがあります。バックエンドでは、イベントがキューに入れられ、*オブジェクト内の提供されたタイムスタンプに基づいて並べ替えが*&#x200B;試みられます`playerTime`。ただし、この機能には制限があります。現在のところ、順序が正しくない呼び出しの間の遅延が 1 秒を超える場合、並べ替えに失敗することがあります。この「許容可能な遅延時間」は、今後の更新では最適化され、設定可能になる可能性があります。
