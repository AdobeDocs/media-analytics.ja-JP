---
title: プレイヤー状態の追跡について
description: ここでは、プレーヤー状態の追跡機能について説明します。この機能には、プレーヤー状態の実装に関する要件やガイドラインなどが含まれます。
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# プレイヤー状態の追跡について

製品体験を最適化してビジネス価値を高めるには、ビデオ視聴時の顧客の行動を把握することが重要です。 これには、様々なプレイヤー状態での滞在時間が含まれます。  また、理解を最適化するには、必要に応じて新しいプレイヤー状態やイベントを作成し、測定する柔軟性が必要です。

プレーヤー状態追跡では、フルスクリーン、クローズドキャプション、ミュート、ピクチャインピクチャ、フォーカスに関する標準のソリューション変数セットを使用して、再生中のビューアのインタラクションをキャプチャできます。  プレイヤー状態の追跡では、カスタムプレーヤー状態を柔軟に作成することもできます。  また、分析の状態追跡変数を、プレイヤーワークスペースのレポートに使用できます。

プレイヤー状態の変更をキャプチャするために、プレイヤー状態追跡はビデオ測定メタデータを更新します。 例えば、「真の」ビデオエンゲージメントを判定するために、プレイヤー状態トラッキングは、サウンドがオフの場合に、または通常とフルスクリーンモードの場合に、サウンドがオンの場合とパッシブの場合、非アクションの場合の時間を測定します。

プレイヤー状態の追跡には、次のような利点があります。

* フルスクリーンやクローズドキャプションなどの一般的な状態を測定する標準変数を提供します。
* 再生セッション中のカスタム状態を測定するためのカスタマイズ可能な変数を提供します。
* カスタムプレイヤーの状態内での滞在時間を測定します。
* 同時に実行される複数の状態を測定します。

![プレイヤー状態の追跡](assets/player_state_tracking.png)

## 要件

プレイヤー状態の追跡には、Adobe Experience Platform(AEP SDK)で使用するMedia Analytics Extensionに対して、次の情報が必要です。
* Web: オーディオおよびビデオ用Adobe Media Analytics(3.x SDK)v1.0以降
* モバイル： オーディオおよびビデオ用Adobe Media Analytics v2.0以降

AEP SDKを使用しない場合は、以下をプレイヤー状態トラッキングで使用できます。
* Media JS SDK 3.0+
* メディアコレクションAPIのバージョン

## ガイドライン

プレイヤー状態の追跡を実装する前に、以下のガイドラインに従ってください。

* プレイヤーの状態は、すべての再生状態で計算されます（分割なし）。
* 複数のプレイヤー状態を同時に測定できます
* 再生中に追跡できるプレイヤー状態の最大数は10です 
* プレイヤー状態指標は、Media Close呼び出しのレポートのためにAnalyticsに送信されます。
* プレイヤーの状態は、個々の再生セッションごとにキャプチャされます。プレイヤーの状態は、プレイバック間で計算されません。 