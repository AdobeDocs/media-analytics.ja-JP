---
title: 標準ステートとカスタムステートについて
description: このトピックでは、プレーヤーステートトラッキング機能と、標準およびカスタムプレーヤーステートの実装と報告に関する要件やガイドラインについて説明します。
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 66%

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

* 1つのビデオセッションは、10個のプレイヤー状態に制限されます。
* 状態の任意の組み合わせが許可されます。
* 複数のプレイヤー状態が通過した場合、最初の10のみが保持され、VA処理コンポーネントの下流に転送されます。
* すべてのステートに対して、終了しているかどうかに関係なく、最大 10 個のステートが適用されます。
* 1つの状態は、複数回開始して終了することができ、1つの状態としてカウントされます。 例えば、5回開始して停止する `closedCapationing` ことはできますが、1つの状態としてカウントされます。
* 許可されている状態の上限が10個を超える状態はすべて破棄されます。

## カスタムステート

カスタムステートの作成機能を使用すると、再生セッション中にカスタムアクションをキャプチャし、カスタムメタデータを更新できます。

カスタム状態の作成について詳しくは、 [メディアAPIリファレンスガイドを参照してください。 `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
