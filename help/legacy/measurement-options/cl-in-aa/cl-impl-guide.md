---
title: カスタムリンクの実装
description: ストリーミングメディアコレクションにカスタムリンクトラッキングを実装する方法を説明します。
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 93%

---

# カスタムリンク導入ガイド {#custom-link-implementation-guide}

カスタムビデオトラッキングでは、Analytics `appMeasurement` 内のカスタムリンクコードを使用した手動リンクトラッキングを使用します。ほとんどの場合、カスタムのビデオリンクビデオトラッキングは、最小のビデオ指標が必要なプラットフォームおよびデバイスで使用します。

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
