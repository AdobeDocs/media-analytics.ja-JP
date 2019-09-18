---
seo-title: カスタムリンク導入ガイド
title: カスタムリンク導入ガイド
uuid: 83315e73-20ca-4db5-9d43-33dade45a13
translation-type: tm+mt
source-git-commit: fe245e766ab8ee48a8e8aaf247cfd552fed816e9

---


# カスタムリンク導入ガイド{#custom-link-implementation-guide}

Custom Video Tracking utilizes [manual link tracking using custom link code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) within Analytics `appMeasurement`. ほとんどの場合、カスタムのビデオリンクビデオトラッキングは、最小のビデオ指標が必要なプラットフォームおよびデバイスで使用します。

* JavaScriptの場合：関 `s.tl()` 数
* モバイルアプリの場合：[trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)、[trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html)、[trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)

* In Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 要件

* ビデオプレーヤー API のイベントおよびデータへのアクセス
* スクリプトを追加できること（分析 SDK を使用している場合）
* （カスタムスクリプトまたはハードコーディングで）トラッキングビーコンを追加できること（Data Insertion API を使用している場合）

## メタデータ

* メタデータは、リンクデータの一部として任意のトラッキングコールに追加できます。
* Remember to update the `linkTrackVars` and `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15’; 
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

* 必要な前提条件が最小限である。
* NoScript を含むあらゆるプラットフォームで動作する。
* 滞在時間や四分位数などの計算はすべてカスタムスクリプトで計算する必要がある。
* 隠されたライブラリやスクリプトがなく、非常に簡単。
* ビデオデータのあらゆる側面に対する完全な制御。
* サンプルプレーヤーへのリンクを削除できる。

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

