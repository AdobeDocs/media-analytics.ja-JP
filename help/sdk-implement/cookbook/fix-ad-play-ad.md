---
title: 広告と広告の間に発生する main:play の解決
description: 広告と広告の間で予期せず発生する main:play 呼び出しを処理する方法を説明します。
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 100%

---

# 広告と広告の間に発生する main:play の解決 {#resolving-main-play-appearing-between-ads}

## 問題点

一部の広告トラッキングシナリオでは、1 つの広告が終了してから次の広告が開始するまでの間に、予期せず `main:play` 呼び出しが発生することがあります。広告完了呼び出しと次の広告開始呼び出しの間の遅延が 250 ミリ秒を超えると、メディア SDK は `main:play` 呼び出しの送信にフォールバックします。この `main:play` へのフォールバックがプリロール広告ブレーク中に発生した場合、コンテンツ開始指標が早期に設定されることがあります。

上記のような広告の間隔は、広告コンテンツとのオーバーラップがないので、メディア SDK ではメインコンテンツとして解釈されます。メディア SDK に広告の情報が設定されず、プレーヤーの状態が再生中になります。広告の情報がなく、プレーヤーの状態が再生中の場合、デフォルトでは、メディア SDK はメインコンテンツの前の間隔であると判断します。情報が null の広告の前の再生時間であると判断することはできません。

## 特定方法

Adobe Debug または Charles などのネットワークパケットスニファーを使用している場合に、プリロール広告ブレーク中に次のハードビートがこのとおりの順序で呼び出されます。

* セッション開始: `s:event:type=start` &amp; `s:asset:type=main`
* 広告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 広告再生: `s:event:type=play` &amp; `s:asset:type=ad`
* 広告完了: `s:event:type=complete` &amp; `s:asset:type=ad`
* メインコンテンツ再生：`s:event:type=play` &amp; `s:asset:type=main` **（想定外）**

* 広告開始: `s:event:type=start` &amp; `s:asset:type=ad`
* 広告再生: `s:event:type=play` &amp; `s:asset:type=ad`
* 広告完了: `s:event:type=complete` &amp; `s:asset:type=ad`
* メインコンテンツ再生：`s:event:type=play` &amp; `s:asset:type=main` **（想定どおり）**

## 解決策

***広告完了呼び出しのトリガーを遅らせます。***

プレーヤー内から間隔を処理するには、最初の広告の `trackEvent:AdComplete` の呼び出しを遅らせ、その直後に 2 つ目の広告の `trackEvent:AdStart` を呼び出します。アプリでは、最初の広告が終了した後の `AdComplete` イベントの呼び出しを遅らせる必要があります。必ず、広告ブレークの最後の広告の `trackEvent:AdComplete` を呼び出します。プレーヤーが現在の広告アセットが広告ブレークの最後の広告であることを識別できる場合は、`trackEvent:AdComplete` を直ちに呼び出します。この解決策では、直前の広告ユニットに関連付けられる広告滞在時間が、1 秒未満ですが増加します。

**プリロールを含む、広告ブレークの開始時：**

* 広告ブレークの `adBreak` オブジェクトのインスタンス（例えば、`adBreakObject`）を作成します。

* `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);` を呼び出します。

**すべての広告アセットの開始時：**

* **を呼び出します`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >これは、前の広告が完了しなかった場合にのみ呼び出してください。ブール値を使用して前の広告の「`isinAd`」状態を維持することを検討してください。

* 広告アセットの広告オブジェクトのインスタンス（例えば、`adObject`）を作成します。
* 広告のメタデータ `adCustomMetadata` を設定します。
* `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);` を呼び出します。
* これがプリロール広告ブレークの最初の広告である場合は、`trackPlay()` を呼び出します。

**すべての広告アセットの完了時：**

* **呼び出しをおこないません**

   >[!NOTE]
   >
   >アプリケーションが広告ブレークの最後の広告であることを認識している場合は、ここで `trackEvent:AdComplete` を呼び出し、`trackEvent:AdBreakComplete` で `trackEvent:AdComplete` の設定をスキップします。

**広告スキップ時：**

* `trackEvent(MediaHeartbeat.Event.AdSkip);` を呼び出します。

**広告ブレークの完了時：**

* **を呼び出します`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >最後の `trackEvent:AdComplete` 呼び出しの一環としてこの手順を既に実行している場合は、この手順をスキップできます。

* `trackEvent(MediaHeartbeat.Event.AdBreakComplete);` を呼び出します。
