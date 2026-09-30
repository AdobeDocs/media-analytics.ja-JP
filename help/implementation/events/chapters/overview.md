---
title: 章とセグメントの追跡
description: メディア SDK を使用したチャプターおよびセグメント追跡の実装方法です。
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
    internal-label: Variables
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 39%
---

# 章とセグメントの追跡

チャプターおよびセグメントの追跡は、カスタム定義されたメディアのチャプターまたはセグメントに対して使用できます。 チャプタートラッキングは一般的に、メディアコンテンツ（野球のイニングなど）に基づくカスタムセグメントの定義や、広告ブレークの間のコンテンツセグメントの定義に使用されます。 コアメディア追跡の実装では、チャプター追跡は&#x200B;**不要です**。

チャプターの追跡には、チャプター開始、チャプター完了、チャプタースキップが含まれます。 カスタマイズされたセグメンテーションロジックでメディアプレーヤーAPIを使用して、チャプターイベントを特定し、チャプター変数を入力します。

## プレーヤーイベント

| プレイヤーイベント | アクション |
| --- | --- |
| 章の開始 | 章オブジェクトを作成し、ChapterStartを呼び出します。 |
| 章完了 | ChapterCompleteを呼び出す |
| 章のスキップ | ChapterSkipを呼び出す |

## 実装手順

1. 章開始イベントがいつ発生するかを特定し、章オブジェクトを作成します。 フィールド定義については、[章名](/help/implementation/variables/chapters/chapter-name.md)、[章の位置](/help/implementation/variables/chapters/chapter-position.md)、[章の長さ](/help/implementation/variables/chapters/chapter-length.md)および[章のオフセット ](/help/implementation/variables/chapters/chapter-offset.md)を参照してください。
1. オプションで、カスタムチャプターメタデータ用のコンテキストデータ変数を作成します。
1. [ チャプター開始](/help/implementation/events/chapters/chapter-start.md)に電話して、チャプターのトラッキングを開始します。
1. 再生がチャプターの終了境界に達したら、[ チャプター完了](/help/implementation/events/chapters/chapter-complete.md)に電話してください。
1. ユーザーが完了前に章をスキップした場合は、[章スキップ ](/help/implementation/events/chapters/chapter-skip.md)を呼び出します。
1. その他の章については、手順1 ～ 5を繰り返します。
