---
title: 移行の概要
description: Media SDK のバージョン 1.x から 2.x への移行について説明します。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 100%

---

# 移行の概要{#migration-overview}

VHL 1.x から VHL 2.x への移行は簡単です。新しいバージョンでは、初期化や設定、プレーヤーのデリゲート用の簡略化された API を利用できるというメリットがあります。

1.x と 2.x の主な違いは次のとおりです。

* **プラグインとデリゲート** - Analytics、VideoPlayer および Heartbeat 用にプラグインやデリゲートを実装する必要がなくなりました。
* **設定** - 1.x のプラグイン用に設定をインスタンス化する必要がなくなりました。

## 2.x のメリット {#benefits-of-two-x}

* すべてのパブリックメソッドは、実装をより簡単にするために、`MediaHeartbeat` クラスに統合されています。
* すべての設定は、`MediaHeartbeatConfig` クラスに統合されました。
* Analytics、VideoPlayer および Heartbeat プラグイン用に設定をインスタンス化する必要はなくなりました。必要なのは、`MediaHeartbeatDelegate` および `MediaHeartbeatConfig` インスタンスを含む `MediaHeartbeat` クラスをインスタンス化するだけです。これは、Media Analytics を初期化するためにのみ必要な実装です。

   `MediaHeartbeat` の初期化により、Analytics Plugin、VideoPlayer Plugin および Heartbeat Plugin 用のすべての実装を安全に削除できます。また、プラグインの配列を入力として取る 初期化のための既存のすべての実装も削除します。1.x と 2.x の実装の違いについて詳しくは、[コードの比較：1.x と 2.x](./code-comparison-1x-2x.md) を参照してください。

2.x の新しい API について詳しくは、「[API 1.x から 2.x への変換](./1x-2x-api-change.md)」を参照してください。
