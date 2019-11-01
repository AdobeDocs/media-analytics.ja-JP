---
title: 広告間に表示されるメイン再生の解決
description: 広告間での予期しないmain:play呼び出しの処理方法。
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 広告と広告の間に発生する main:play の解決{#resolving-main-play-appearing-between-ads}

## 問題点

一部の広告トラッキングシナリオでは、1 つの広告が終了してから次の広告が開始するまでの間に、予期せず `main:play` 呼び出しが発生することがあります。If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. この `main:play` へのフォールバックがプリロール広告ブレーク中に発生した場合、コンテンツ開始指標が早期に設定されることがあります。

上記のような広告の間隔は、広告コンテンツとのオーバーラップがないので、メディア SDK ではメインコンテンツとして解釈されます。メディア SDK に広告の情報が設定されず、プレーヤーの状態が再生中になります。広告の情報がなく、プレーヤーの状態が再生中の場合、デフォルトでは、メディア SDK はメインコンテンツの前の間隔であると判断します。情報が null の広告の前の再生時間であると判断することはできません。

## 特定方法

Adobe DebugまたはCharlesなどのネットワークパケットスニファーを使用している間、プリロール広告の時間中に次のハートビート呼び出しがこの順序で表示される場合：

* セッション開始: `s:event:type=start` &amp; `s:asset:type=main`
* 広告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 広告再生: `s:event:type=play` &amp; `s:asset:type=ad`
* 広告完了: `s:event:type=complete` &amp; `s:asset:type=ad`
* メインコンテンツの再生： `s:event:type=play` &amp; `s:asset:type=main`**（予期しない）**

* 広告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 広告再生: `s:event:type=play` &amp; `s:asset:type=ad`
* 広告完了: `s:event:type=complete` &amp; `s:asset:type=ad`
* メインコンテンツの再生： `s:event:type=play` &amp; `s:asset:type=main`(期&#x200B;**待値)**

## 解決策

***広告完了呼び出しのトリガーを遅らせます。***

プレーヤー内から間隔を処理するには、最初の広告の `trackEvent:AdComplete` の呼び出しを遅らせ、その直後に 2 つ目の広告の `trackEvent:AdStart` を呼び出します。アプリでは、最初の広告が終了した後の `AdComplete` イベントの呼び出しを遅らせる必要があります。必ず、広告ブレークの最後の広告の `trackEvent:AdComplete` を呼び出します。プレーヤーが現在の広告アセットが広告ブレークの最後の広告であることを識別できる場合は、`trackEvent:AdComplete` を直ちに呼び出します。この解決策では、直前の広告ユニットに関連付けられる広告滞在時間が、1 秒未満ですが増加します。

**プリロールを含む、広告ブレークの開始時：**

* 広告ブレークの `adBreak` オブジェクトのインスタンス（例えば、`adBreakObject`）を作成します。

* 呼び出し `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**すべての広告アセットの開始時：**

* **通話`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >前の広告が完了していない場合にのみ呼び出します。 ブール値を使用して前の広告の「`isinAd`」状態を維持することを検討してください。

* 広告アセットの広告オブジェクトのインスタンス（例えば、`adObject`）を作成します。
* Populate the ad metadata, `adCustomMetadata`.
* 呼び出し `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**すべての広告アセットの完了時：**

* **電話をかけない**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**広告スキップ時：**

* 呼び出し `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**広告ブレークの完了時：**

* **通話`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* 呼び出し `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

