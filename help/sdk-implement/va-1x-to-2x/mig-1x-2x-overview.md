---
seo-title: 移行の概要
title: 移行の概要
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# 移行の概要{#migration-overview}

VHL 1.x から VHL 2.x への移行は簡単です。新しいバージョンでは、初期化や設定、プレーヤーのデリゲート用の簡略化された API を利用できるというメリットがあります。

1.x と 2.x の主な違いは次のとおりです。

* **プラグインとデリゲート** - Analytics、VideoPlayer および Heartbeat 用にプラグインやデリゲートを実装する必要がなくなりました。
* **設定** - 1.x のプラグイン用に設定をインスタンス化する必要がなくなりました。

## 2.xのメリット {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Analytics、VideoPlayerおよびHeartbeatプラグインの設定をインスタンス化する必要はなくなりました。 必要なのは、インスタンスと共にクラスを `MediaHeartbeat` インスタンス化 `MediaHeartbeatDelegate` する `MediaHeartbeatConfig` ことだけです。 これは、Media Analyticsの初期化に必要な唯一の実装です。

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. また、プラグインの配列を入力として取る 初期化のための既存のすべての実装も削除します。You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

2.x の新しい API について詳しくは、「[API 1.x から 2.x への変換](./1x-2x-api-change.md)」を参照してください。
