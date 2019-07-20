---
seo-title: 品質パラメーター
title: 品質パラメーター
uuid: 0d9fa764- evdef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# 品質パラメーター{#quality-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集する Quality of Experience（QoE／QoS）データを示します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *Send With（次を含む* ）-データの送信日時を示します。 *メディア開始* はメディア開始時に送信される解析呼び出し、 *広告開始* は広告開始時に送信される解析呼び出し、など。 *閉じる* 呼び出しは、ハートビートサーバーからメディアセッションの最後、または広告、チャプターなどの最後に直接送信されるコンパイルされた解析呼び出しです。閉じる呼び出しはネットワークパケット呼び出しでは使用できません。
   * *最小のSDK のバージョン* - パラメーターにアクセスするのに必要な SDK のバージョン。
   * *値の例* - 変数の一般的な利用方法の例。
* **ネットワークパラメーター：** Adobe Analytics またはハートビートサーバーに渡される値。この列には、Adobe Media SDK によって生成されるネットワーク呼び出しに含まれるパラメーターの名前が示されています。
* **レポート：**&#x200B;ビデオデータの確認方法と分析方法に関する詳細。
   * *利用可能* - デフォルトでもデータをレポートで確認できる場合は&#x200B;*可*、カスタム設定が必要な場合は&#x200B;*カスタム*。
   * *予約変数* - 予約変数で取得されるデータの形式（イベント、eVar、prop または分類）。
   * *レポート名* - Adobe Aanlytics の変数のレポート名。
   * *コンテキストデータ* - レポートサーバーに渡され、処理ルールで使用される Adobe Analytics のコンテキストデータの名前。
   * *データフィード* - クリックストリームまたはライブストリームデータフィード内の変数の列の名前。
   * *Audience Manager* - Adobe Audience Manager 内の特性名。

## 品質メタデータ {#section_8467F9729DA04A888A2657712234D7C7}

### 平均ビットレート

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.qoe.bitrate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 800~899 </li><li> **説明:**<br/>平均ビットレート（kbps）。値は、100 kbps の間隔で事前定義されたグループです。平均ビットレートは、再生セッション中に発生した再生時間に関連するすべてのビットレート値の加重平均として計算されます。を参照してください。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bitrateAverageBucket） </li> <li> **ハートビート:**<br/> （l:stream:bitrate） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>平均ビットレート </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bitrateAverageBucket） </li> <li> **データフィード：**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bitrateAverageBucket） </li> </ul> |



### 開始時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.timeToStart </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 30,000 </li><li> **説明:**<br/>QoSObjectを使用して設定しない場合、この値はデフォルトでゼロになります。この値はミリ秒単位で設定します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>timeToStart) </li> <li> **ハートビート:**<br/> （l:stream:startup_ time） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>開始時間 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>timeToStart) </li> <li> **データフィード：**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.framesPerSecond </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 24 </li><li> **説明:**<br/>ストリームフレームレートの現在の値（フレーム/秒）。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **ハートビート:**<br/> （l:stream:fps） </li> </ul> | <ul> <li> **利用可能：**<br/>不可 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



### ドロップフレーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>droppedFrames </li> <li> **API キー：**<br/>media.qoe.droppedFrames </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 3 </li><li> **説明:**<br/>ドロップフレームの数（整数）。この値は、再生セッション中のすべてのドロップフレームの合計として計算されます。この値は、最後の値（l:stream:dropped_ frames.）  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>droppedFrameCount） </li> <li> **ハートビート:**<br/> （l:stream:<br/>dropped_ frames） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ドロップフレーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>droppedFrameCount） </li> <li> **データフィード：**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>droppedFrameCount） </li> </ul> |



### バッファーイベント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 2 </li><li> **説明:**<br/>バッファーイベントの数。この指標は、再生セッション中に発生した複数のバッファー状態の総数として計算されます。プレーヤーが他の状態（再生、一時停止など）からバッファー状態に移行した回数となります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bufferCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= buffer） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>バッファーイベント </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bufferCount） </li> <li> **データフィード：**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bufferCount） </li> </ul> |



### 合計バッファー時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK バージョン：** </li> <li> **サンプル値:**<br/> 30 </li><li> **説明:**<br/>バッファリングの合計時間（秒単位）。この値は、再生セッション中に発生したすべてのバッファーイベントの時間の合計として計算されます。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bufferTime） </li> <li> **ハートビート:**<br/> （l:イベント:duration） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>合計バッファー時間 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bufferTime） </li> <li> **データフィード：**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bufferTime） </li> </ul> |



### ビットレート変更

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.bitrateChange </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 3 </li><li> **説明:**<br/>ビットレート変更の数（整数）。この値は、再生セッション中に発生したすべてのビットレート変更イベントの合計として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bitrateChangeCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= bitrate_ change） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビットレート変更 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bitrateChangeCount） </li> <li> **データフィード：**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bitrateChangeCount） </li> </ul> |



### エラー／エラーイベント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1 </li><li> **説明:**<br/>エラーの数が発生しました（整数）。この値は、再生セッション中に発生したすべてのエラーイベントの合計として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>errorCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>errorCount） </li> <li> **データフィード：**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>errorCount） </li> </ul> |



### プレーヤー SDK のエラー ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>プレイヤーSDKによって生成される一意のエラーID。お客様は、実装時に提供されたエラー API を使用してエラーコードや ID を指定する必要があります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>PlayerSDKErrors） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>PlayerSDKErrors） </li> <li> **データフィード:**<br/> videoqoeplayersdkerror </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>PlayerSDKErrors） </li> </ul> |



### 外部エラー ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>外部ソースからの一意のエラーID（CDNエラーなど）。お客様は、実装時に提供されたエラー API を使用してエラーコードや ID を指定する必要があります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>ExternalErrors） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>ExternalErrors） </li> <li> **データフィード:**<br/> videoqoeextnererrors </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>ExternalErrors） </li> </ul> |



### メディア SDK のエラー ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>再生中にMedia SDKによって生成される一意のエラーID。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>MediaDKErrors） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>MediaDKErrors） </li> <li> **データフィード：**<br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>MediaDKErrors） </li> </ul> |




### セッション終了 {#session-end}

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 2.1 </li> <li> **サンプル値:**<br/> end </li><li> **説明:**<br/>endイベントは、SDKがバックエンドへのclose呼び出しを送信していることを意味します。バックエンドがこのイベントを受信すると、そのビデオのセッションを終了し、それ以上処理をおこないません。<br/>メディアが100%に完了した場合は、関連情報の `s:event:type=complete.`[「コンテンツの完了」を](audio-video-parameters.md#content-complete) 参照してください。 </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート:**<br/> （s:イベント:type= end） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



## 品質指標 {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### 開始時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 30,000 </li><li> **説明:**<br/>QoSObjectを使用して設定しない場合、この値はデフォルトでゼロになります。この値はミリ秒単位で設定します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>timeToStart) </li> <li> **ハートビート:**<br/> （l:stream:startup_ time） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>開始時間 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>timeToStart) </li> <li> **データフィード：**<br/>videoqoetimetostart </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### バッファーイベント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 2 </li><li> **説明:**<br/>バッファーイベント数（整数）。この指標は、再生セッション中に発生したバッファーイベントの総数として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bufferCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= buffer） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>バッファーイベント </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bufferCount） </li> <li> **データフィード：**<br/>videoqoebuffercount </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bufferCount） </li> </ul> |



### 合計バッファー時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 15 </li><li> **説明:**<br/>バッファリングの合計滞在時間（秒単位）integer）を使用します。この値は、再生セッション中に発生したすべてのバッファーイベントの時間の合計として計算されます。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bufferTime） </li> <li> **ハートビート:**<br/> （l:イベント:duration） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>合計バッファー時間 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bufferTime） </li> <li> **データフィード：**<br/>videoqoebuffertime </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bufferTime） </li> </ul> |



### ビットレート変更

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>イベント </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> "3" </li><li> **説明:**<br/>ビットレートの変更数。この値は、再生セッション中に発生したすべてのビットレート変更イベントの合計として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bitrateChangeCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= bitrate_ change） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ビットレート変更 </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bitrateChangeCount） </li> <li> **データフィード：**<br/>videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bitrateChangeCount） </li> </ul> |



### エラー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1 </li><li> **説明:**<br/>発生したエラーの数（整数）。この値は、再生セッション中に発生したすべてのエラーイベントの合計として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>errorCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>エラーイベント </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>errorCount） </li> <li> **データフィード：**<br/>videoqoeerrorcount </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>errorCount） </li> </ul> |



### ドロップフレーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1 </li><li> **説明:**<br/>ドロップフレームの数（整数）。この値は、再生セッション中のすべてのドロップフレームの合計として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>droppedFrameCount） </li> <li> **ハートビート:**<br/> （l:stream:<br/>dropped_ frames） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ドロップフレーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>droppedFrameCount） </li> <li> **データフィード：**<br/>videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>droppedFrameCount） </li> </ul> |



### 開始前にドロップ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>ユーザーが開始前にビデオを終了した回数。この指標は、広告とは無関係に、コンテンツがレンダリングされなかった場合に 1 に設定されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>dropBeforeStart） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= aa_ start） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>開始前にドロップ </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>dropBeforeStart） </li> <li> **データフィード：**<br/>videoqoedropbeforestart </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>dropBeforeStart） </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### バッファーの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>バッファリングの影響を受けたストリームの数。この指標は、再生セッション中に少なくとも 1 つのバッファーイベントが発生した場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>buffer) </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= buffer） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>バッファーの影響を受けたストリーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>buffer) </li> <li> **データフィード：**<br/>videoqoebuffer </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### ビットレート変更の影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>ビットレートの変更が発生したストリームの数。この指標は、再生セッション中に少なくとも 1 つのビットレート変更イベントが発生した場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>BitrateChange） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= bitrate_ change） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ビットレート変更の影響を受けたストリーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>BitrateChange） </li> <li> **データフィード：**<br/>videoqoebitratechange </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>BitrateChange） </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### 平均ビットレート

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 3200 </li><li> **説明:**<br/>平均ビットレート（kbps、整数）。この指標は、再生セッション中に発生した再生時間に関連するすべてのビットレート値の加重平均として計算されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>bitrateAverage） </li> <li> **ハートビート:**<br/> （l:stream:bitrate） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>平均ビットレート </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>bitrateAverage） </li> <li> **データフィード：**<br/>videoqoebitrateaverage </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>bitrateAverage） </li> </ul> |



### エラーの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>ビットレートの変更が発生したストリームの数。この指標は、再生セッション中に少なくとも 1 つのビットレート変更イベントが発生した場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>error） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= error） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>エラーの影響を受けたストリーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>error） </li> <li> **データフィード：**<br/>videoqoeerror </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>error） </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### ドロップフレームの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>フレームがドロップされたストリームの数。この指標は、再生セッション中に少なくとも 1 つのフレームがドロップした場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>droppedFrames) </li> <li> **ハートビート:**<br/> （l:stream:<br/>dropped_ frames） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ドロップフレームの影響を受けたストリーム </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>droppedFrames) </li> <li> **データフィード：**<br/>videoqoedroppedframes </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### 停止の影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>停止したイベントが発生したストリームの数。この指標は、再生セッション中に少なくとも 1 回、停止が発生した場合にのみ 1 に設定されます。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>stall) </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= stall） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> **データフィード：**<br/>なし </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。このイベントを設定しない場合は、値が送信されません。

### 停止イベント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> **サンプル値:**<br/> "3" </li><li> **説明:**<br/>再生セッション中に再生が停止した回数。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>stallCount） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= stall） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>stallCount） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>stallCount） </li> </ul> |



### 合計停止時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> **サンプル値:**<br/> 12 </li><li> **説明:**<br/>合計時間（秒単位）整数）再生セッション中に再生が停止した。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. qoe.<br/>stallTime） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= stall） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. qoe.<br/>stallTime） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. qoe.<br/>stallTime） </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

