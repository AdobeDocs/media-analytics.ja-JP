---
title: テスト 2 メディアの中断
description: 検証で使用するメディア中断テストについて説明します。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 100%

---

# テスト 2：メディアの中断{#test-media-interruption}

このテストケースは、モバイルの中断動作を検証します。

## テスト手順

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレーヤーを開始する**

   メディアプレーヤーの開始時に、次の順番で呼び出しが送信されます。

   1. Adobe Analytics（AppMeasurement）Start
   1. Media Analytics（ハートビート）Start
   1. Media Analytics（ハートビート）Adobe Analytics Start 呼び出しがリクエストされる

   上記の最初の 2 つの呼び出しには、追加のメタデータおよび変数が含まれます。呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#start-the-media-player)を参照してください。

   上記の 3 番目の呼び出しは、Adobe Analytics サーバーに送信される Adobe Analytics Start 呼び出し（`pev2=ms_s`）をメディア SDK がリクエストしたことを Media Analytics サーバーに伝えます。

1. **メインコンテンツを中断せずに 5 分以上間再生する**

   **コンテンツの再生**

   コンテンツの再生中、メディア SDK は、10 秒ごとに再生呼び出し（ハートビート）を Media Analytics サーバーに送信します。

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#play-main-content)を参照してください。

   また、これらの広告呼び出しの追加情報については、お使いのプラットフォームの[広告の追跡](/help/use-cases/track-ads/track-ads-overview.md)の手順も参照してください。

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   アプリがバックグラウンドで実行されている間、`main:pause` 呼び出しのみが Media Analytics サーバーに送信される必要があります（VHL バージョン 1.6.6 以降）。

1. **アプリまたはブラウザーをフォアグラウンドに移動する**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **メインコンテンツメディアを中断せずに 5 分以上間再生する**

   呼び出しパラメーターおよびメタデータについては、[テスト呼び出しの詳細](/help/legacy/validation/test-call-details.md#play-main-content)を参照してください。

1. **メディアプレーヤーを閉じる**

   メディアプレーヤーが閉じられた後は、追加のトラッキングコールを発生させないでください。
