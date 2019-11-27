---
title: マイルストーンからカスタムリンクへの移行
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# マイルストーンからカスタムリンクへの移行 {#migrating-from-milestone-to-custom-link}

## 概要 {#overview}

マイルストーンとカスタムリンクのトラッキングでは、ビデオ測定の中核的な概念は同じです。ビデオプレーヤーのイベントを取得して分析メソッドにマッピングする一方で、プレーヤーのメタデータおよび値を取得して分析変数にマッピングします。カスタムリンクのアプローチは、実装と収集されるデータの両方の縮小と簡素化と考えてください。カスタムリンクソリューションを使用する場合、ビデオ測定用の変数やメソッドが事前に定義されていないので、完全なカスタムのセットアップが必要です。開始や完了など、基本的なプレーヤーイベントについては、カスタムリンクのトラッキングコールを指すようにプレーヤーのイベントコードを更新できる必要があります。詳しくは、[カスタムリンク導入ガイド](/help/measurement-options/cl-in-aa/cl-impl-guide.md)および[カスタムリンクコードを使用した手動リンクトラッキング](https://marketing.adobe.com/resources/help/ja_JP/sc/implement/link_manual.html)を参照してください。

以下の表では、マイルストーンソリューションとカスタムリンクソリューション間の変更について説明します。

## 移行ガイド {#migration-guide}

### ビデオ変数リファレンス

<table>
<thead>
<tr>
<th><strong>マイルストーンの指標</strong></th>
<th><strong>変数の種類</strong></th>
<th><strong>カスタムリンク</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>コンテンツ</td>
<td>
<p>eVar</p>
<p>デフォルトの有効期限：訪問</p>
</td>
<td>独自の eVar を定義する</td>
</tr>
<tr>
<td>コンテンツタイプ</td>
<td>
<p>eVar</p>
<p>デフォルトの有効期限：ページビュー</p>
</td>
<td>独自の eVar を定義する</td>
</tr>
<tr>
<td>コンテンツ視聴時間</td>
<td>
<p>event</p>
<p>タイプ：カウンター</p>
</td>
<td>独自のイベントを定義する</td>
</tr>
<tr>
<td>ビデオ開始</td>
<td>
<p>event</p>
<p>タイプ：カウンター</p>
</td>
<td>独自のイベントを定義する</td>
</tr>
<tr>
<td>ビデオ完了</td>
<td>
<p>event</p>
<p>タイプ：カウンター</p>
</td>
<td>独自のイベントを定義する</td>
</tr>
</tbody>
</table>

### メディアモジュール変数

<table>
<thead>
<tr>
<th>マイルストーン
</th>
<th>マイルストーンの構文
</th>
<th>カスタムリンク
</th>
<th>カスタムリンク構文
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = {
  "a.media.name":
    "eVar2,prop2",
  "a.media.segment":
    "eVar3",
  "a.contentType":
    "eVar1",
  "a.media.timePlayed":
    "event3",
  "a.media.view":
    "event1",
  "a.media.segmentView":
    "event2",
  "a.media.complete":
    "event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>該当なし
</td>
<td>コンテキストデータの eVar、prop およびイベントへのマッピングは処理ルールによって実施されるようになりました。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>マイルストーン
</th>
<th>マイルストーンの構文
</th>
<th>カスタムリンク
</th>
<th>カスタムリンク構文
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>該当なし
</td>
<td>コンテキストデータの eVar、prop およびイベントへのマッピングは処理ルールによって実施されるようになりました。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

### オプションの変数

<table>
<thead>
<tr>
<th>マイルストーン
</th>
<th>マイルストーンの構文
</th>
<th>カスタムリンク
</th>
<th>カスタムリンク構文
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
    = 1
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Custom Player Name"
</pre>
</td>
<td>
リンクの呼び出しで eVar またはコンテキストデータ変数を設定する
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones 
  = "20,40,60";
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
  = true;
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
</tbody>
</table>

### 広告トラッキング変数

<table>
<thead>
<tr>
<th>マイルストーン
</th>
<th>マイルストーンの構文
</th>
<th>カスタムリンク
</th>
<th>カスタムリンク構文
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones 
    = "20,40,60";
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
    = true;
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
    = true;
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
</tbody>
</table>

### メディアモジュールメソッド

<table>
<thead>
<tr>
<th>マイルストーン
</th>
<th>マイルストーンの構文
</th>
<th>カスタムリンク
</th>
<th>カスタムリンク構文
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName：</b>（必須）ビデオレポートに表示するビデオの名前。</td>
<td>リンクの呼び出しで eVar またはコンテキストデータ変数を設定する</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength：</b>（必須）ビデオの長さ（秒単位）。
</td>
<td>
リンクの呼び出しで eVar またはコンテキストデータ変数を設定する
</td>
<td>
<pre>
s.contextData['video.length']
  = ”90”;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName：</b>（必須）ビデオの視聴に使用されるメディアプレーヤーの名前。ビデオレポートに表示する名前です。
</td>
<td>
リンクの呼び出しで eVar またはコンテキストデータ変数を設定する
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>該当なし
</td>
<td>使用不可</td>
</tr>
<tr>
<td>name</td>
<td><b>name：</b>（必須）広告の名前または ID。</td>
<td>該当なし</td>
<td>使用不可</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length：</b>（必須）広告の長さ。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName：</b>（必須）広告の表示に使用するメディアプレーヤーの名前。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName：</b>広告が埋め込まれたプライマリコンテンツの名前または ID。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod：</b>広告が表示されたプライマリコンテンツ内の位置。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition：</b>広告が表示されるポッド内の位置。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM：</b>この再生に適用される CPM または暗号化された CPM（「~」のプレフィックスが付く）。
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
</td>
<td>カスタムリンクの分析呼び出しを使用してクリックを追跡する
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
s.tl()
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>該当なし 
</td>
<td>使用不可
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
リンクの呼び出しで eVar またはコンテキストデータ変数を設定する
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>該当なし
</td>
<td>使用不可
</td>
</tr>
</tbody>
</table>

