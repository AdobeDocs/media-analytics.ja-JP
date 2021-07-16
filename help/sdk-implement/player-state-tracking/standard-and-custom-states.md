---
title: 標準ステートとカスタムステートについて
description: 標準プレーヤーステートとカスタムプレーヤーステートの実装とレポートに関する要件やガイドラインを含め、プレーヤーステートトラッキング機能について説明します。
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 100%

---

# 標準ステートとカスタムステートについて

5 つの標準プレーヤーステートがあり、独自のカスタムステートを追加できます。

| 標準のステート名 | メディア SDK の定数 | メディアコレクション API の名前 |
|-----------------------|------------------------------------------|-----------------------------|
| フルスクリーン | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| クローズドキャプション | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| ミュート | `ADB.Media.PlayerState.Mute` | `mute` |
| ピクチャーインピクチャー | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| フォーカス設定 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

標準ステートとカスタムステートではデータの計算方法は同じですが、Analytics レポートではデータの保存方法が異なります。

**標準ステートの場合**：Analyticsレポート（管理者側）のメディア管理コンソールからプレーヤーステートトラッキングを有効にした場合、15 個のソリューション変数をレポートおよびデータの書き出しに使用できます。

**カスタムステートの場合**：独自の処理ルールを作成して、計算した値をカスタムイベントに保存し、それらのルールをレポートおよびデータの書き出しに使用できます。

## ガイドライン

* 1 つのビデオセッションでは、最大 10 のプレーヤーステートを使用できます。
* ステートの組み合わせは自由です。
* 複数のプレーヤーステートが渡されると、最初の 10 個のみが保持され、ダウンストリームの VA処理コンポーネントへと転送されます。
* すべてのステートに対して、終了しているかどうかに関係なく、最大 10 個のステートが適用されます。
* 1 つのステートは、複数回開始および終了でき、1 つのステートとしてカウントされます。例えば、`closedCapationing` は開始と停止を 5 回繰り返すことができますが、1 つのステートとしてカウントされます。
* 許可されているステートの最大数である 10 を超えるステートは、すべて破棄されます。

## カスタムステート

カスタムステートの作成機能を使用すると、再生セッション中にカスタムアクションをキャプチャし、カスタムメタデータを更新できます。

カスタムステートの作成について詳しくは、[メディア API リファレンスガイド`createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)を参照してください。
