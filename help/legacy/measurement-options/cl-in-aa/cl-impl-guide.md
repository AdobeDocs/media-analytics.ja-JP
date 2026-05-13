---
title: カスタムリンクの実装
description: ストリーミングメディアサービスにカスタムリンクトラッキングを実装する方法について説明します。
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/5N4rGrJDjkAGzRZJj6SMElP2EJq-QZjh7JLgDoKxiOo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 206
ht-degree: 94%

---

# カスタムリンク導入ガイド{#custom-link-implementation-guide}

カスタムビデオトラッキングでは、Analytics `appMeasurement` 内のカスタムリンクコードを使用した手動リンクトラッキングを使用します。
ほとんどの場合、カスタムのビデオリンクビデオトラッキングは、最小のビデオ指標が必要なプラットフォームおよびデバイスで使用します。

* JavaScript の場合：`s.tl()` 関数
* モバイルアプリの場合：[trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=ja)、[trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=ja)、[trackAction() OTT](/help/use-cases/analytics-with-ott/track-app-actions.md)
* Data Insertion API の場合：[linktype タグ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 要件

* ビデオプレーヤー API イベントとデータへのアクセス
* Analytics SDK を使用する場合のスクリプトの追加機能
* データ挿入 API を使用する場合に、トラッキングビーコン（カスタムスクリプティングまたはハードコード）を追加する機能

## メタデータ

* メタデータは、リンクデータの一部として任意のトラッキングコールに追加できます。
* `linkTrackVars` および `linkTrackEvents` を必ず更新してください。

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## カスタムリンクを使用する理由

* 必要最小限の前提条件
* NoScript を含むあらゆるプラットフォームで動作する。
* 滞在時間や四分位数などの計算は、カスタムスクリプトで計算する必要があります
* 隠されたライブラリやスクリプトがなく、非常に簡単。
* ビデオデータのあらゆる側面に対する完全な制御。

## HTML5 プレーヤー用のサンプル JavaScript

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```
