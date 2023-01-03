---
title: プレーヤーステートトラッキングについて
description: プレーヤーステートの実装とレポートに関する要件やガイドラインを含め、プレーヤーステートのトラッキング機能について説明します。
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 100%

---

# プレーヤーステートトラッキングについて

製品エクスペリエンスを最適化してビジネス価値を高めるには、ビデオ視聴時の顧客の行動を把握することが重要です。これには、様々なプレーヤーステートでの滞在時間が含まれます。また、必要に応じて、新しいプレーヤーステートやイベントを作成および測定する柔軟性も重要です。

プレーヤーステートトラッキングでは、フルスクリーン、クローズドキャプション、ミュート、ピクチャインピクチャ、フォーカス設定に関する標準のソリューション変数セットを使用して、再生中の閲覧者のインタラクションをキャプチャできます。プレーヤーステートトラッキングでは、カスタムプレーヤーステートを柔軟に作成することもできます。Analysis Workspace のレポートに、プレーヤーステートトラッキング変数を使用できます。

プレーヤーステートの変更を取得するために、プレーヤーステートトラッキングでは、ビデオ測定メタデータを更新します。例えば、「真の」ビデオエンゲージメントを判定するために、プレーヤーステートトラッキングでは、音声がオンとなっている場合の滞在時間と音声がオフになっている場合の受動的な（積極的でない）ビデオ視聴、または標準モードとフルスクリーンモードでの滞在時間を比較します。

プレーヤーステートトラッキングには、次のような利点があります。

* フルスクリーンやクローズドキャプションなどの一般的なステートを測定する標準変数を提供します。
* 再生セッション中のカスタムステートを測定するための、カスタマイズ可能な変数を提供します。
* カスタムプレーヤーステート内での滞在時間を測定します。
* 同時に発生する複数のステートを測定します。

![プレーヤーステートトラッキング](assets/player_state_tracking.png)

## 要件

プレーヤーステートトラッキングでは、データ収集をおこなうために、次のいずれかが必要です。
* メディア JS SDK 3.0 以降
* Adobe Experience Cloud ソリューション向け Chromecast 3.0 SDK
* Media Analytics 拡張機能（Adobe Experience Platform（AEP）SDK 用）
   * Web：Adobe Media Analytics (3.x SDK) for Audio and Video v1.0 以降
   * モバイル：Adobe Media Analytics for Audio and Video v2.0 以降
* メディアコレクション API

## ガイドライン

プレーヤーステートトラッキングを実装する前に、以下のガイドラインを考慮してください。

* プレーヤーステートは、すべての再生ステートで（分割せずに）計算されます。
* 複数のプレーヤーステートを同時に測定できます.
* 再生中に追跡できるプレーヤーステートの最大数は 10 個です
* プレーヤーステート指標は、メディア終了呼び出しを報告する際にのみ、Analytics に送信されます。
* ステートの停止後、アプリケーションのステータスに関する情報は保持されません。ステートの終了後にトラッキングを続行するには、ステートを再び開始する必要があります。プレーヤーは、再生ステートごとにステートを再び開始する必要があります。
* プレーヤーステートは、個々の再生セッションごとにキャプチャされ、再生をまたいでは計算されません。