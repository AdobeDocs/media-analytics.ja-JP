---
title: 標準状態とカスタム状態について
description: このトピックでは、プレーヤーの標準およびレポートの状態を実装するための要件やガイドラインを含む、プレーヤー状態追跡機能について説明します。
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# 標準状態とカスタム状態について

5つの標準プレーヤー状態が使用可能で、独自のカスタム状態を追加できます。

| 標準の州名 | メディアSDKの定数 | メディアコレクションAPI名 |
|-----------------------|------------------------------------------|-----------------------------|
| フルスクリーン | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| クローズドキャプション | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| ミュート | `ADB.Media.PlayerState.Mute` | `mute` |
| 図の表示 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| フォーカス中 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

データは、標準状態とカスタム状態で同じ方法で計算されますが、Analyticsレポートではデータの保存方法が異なります。

**標準状態の場合**- Analyticsレポート（管理者側）のメディア管理コンソールからプレイヤー状態の追跡を有効にした場合、15個のソリューション変数をレポートおよびデータのエクスポートに使用できます。

**カスタム状態の場合**— 独自の処理ルールを作成して、計算した値をカスタムイベントに格納し、それらのルールをレポートおよびデータのエクスポートに使用できます。

## ガイドライン

* 1つのビデオセッションは、10個のプレイヤー状態に制限されます。
* 状態の任意の組み合わせが許可されます。
* 複数のプレイヤー状態が通過した場合、最初の10のみが保持され、VA処理コンポーネントの下流に転送されます。
* 最大10個の状態は、閉じているかどうかに関係なく、すべての状態に適用されます。
* 1つの状態は、複数回開始して終了することができ、1つの状態としてカウントされます。 例えば、5回開始して停止する `closedCapationing` ことはできますが、1つの状態としてカウントされます。
* 許可されている状態の上限が10個を超える状態はすべて破棄されます。

## カスタム状態

カスタム状態を作成する機能を使用すると、再生セッション中にカスタムアクションをキャプチャし、カスタムメタデータを更新できます。

カスタム状態の作成について詳しくは、 [メディアAPIリファレンスガイドを参照してください。 `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
