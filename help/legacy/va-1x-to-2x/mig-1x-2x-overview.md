---
title: 移行の概要
description: Media SDK のバージョン 1.x から 2.x への移行について説明します。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 87%

---

# VHL 1.x から VHL 2.x へのレガシー移行の概要 {#migration-overview}

VHL 1.x から VHL 2.x への移行は簡単です。新しいバージョンでは、初期化や設定、プレーヤーのデリゲート用の簡略化された API を利用できるというメリットがあります。

1.x と 2.x の主な違いは次のとおりです。

* **プラグイン、デリゲート -** Analytics、VideoPlayer、ハートビート用のプラグインとデリゲートを実装する必要がなくなりました。
* **設定 –** 1.x プラグインの設定をインスタンス化する必要がなくなりました。

## 2.x のメリット {#benefits-of-two-x}

* すべてのパブリックメソッドは、実装をより簡単にするために、`MediaHeartbeat` クラスに統合されています。
* すべての設定は、`MediaHeartbeatConfig` クラスに統合されました。
* Analytics、VideoPlayer および Heartbeat プラグイン用に設定をインスタンス化する必要はなくなりました。 必要なのは、`MediaHeartbeatDelegate` および `MediaHeartbeatConfig` インスタンスを含む `MediaHeartbeat` クラスをインスタンス化するだけです。 これは、Media Analytics を初期化するためにのみ必要な実装です。

  `MediaHeartbeat` の初期化により、Analytics Plugin、VideoPlayer Plugin および Heartbeat Plugin 用のすべての実装を安全に削除できます。 また、プラグインの配列を入力として取る 初期化のための既存のすべての実装も削除します。 1.x と 2.x の実装の違いについて詳しくは、[コードの比較：1.x と 2.x](./code-comparison-1x-2x.md) を参照してください。

2.x の新しい API について詳しくは、「[API 1.x から 2.x への変換](./1x-2x-api-change.md)」を参照してください。
