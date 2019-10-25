---
seo-title: 品質パラメーター
title: 品質パラメーター
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 44b12731c4a701f0f2536c1c83a9ad4a8b27b49b

---


# 品質パラメーター{#quality-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集する Quality of Experience（QoE／QoS）データを示します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *Sent With* — データが送信されるタイミングを示します。 *Media Start* は、メディア開始時に送信される解析呼び出し、 *Ad Start* は、広告開始時に送信される解析呼び出しなどです。close呼び出し *は* 、メディアセッションの終了時、または広告やチャプターの終わりなどに、ハートビートサーバーからAnalyticsサーバーに直接送信される、コンパイル済みのAnalytics呼び出しです。 閉じる呼び出しは、ネットワークパケット呼び出しでは使用できません。
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

## 品質メタデータ {#quality-metadata}

### 平均ビットレート

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.qoe.bitrate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：800-899 </li><li> **説明：平**<br/>均ビットレート(kbps)。 値は、100 kbps の間隔で事前定義されたグループです。平均ビットレートは、再生セッション中に発生した再生時間に関連するすべてのビットレート値の加重平均として計算されます。を参照してください。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> ハートビート：(l:stream:bitrate) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>平均ビットレート </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **データフィード：**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bitrateAverageBucket) </li> </ul> |


### 開始時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.timeToStart </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：30,000 </li><li> **説明：QoSObject**<br/>を使用して設定しない場合、この値のデフォルトは0です。 この値はミリ秒単位で設定します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> ハートビート：(l:stream:startup_time) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>開始時間 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>timeToStart) </li> <li> **データフィード：**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>timeToStart) </li> </ul> |


### FPS

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.framesPerSecond </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：24 </li><li> **説明：ス**<br/>トリームフレームレートの現在の値（フレーム/秒）。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> ****<br/> ハートビート：(l:stream:fps) </li> </ul> | <ul> <li> **利用可能：**<br/>不可 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager：**<br/> </li> </ul> |



### ドロップフレーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>droppedFrames </li> <li> **API キー：**<br/>media.qoe.droppedFrames </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：3 </li><li> **説明：ド**<br/>ロップフレームの数（整数）。 この値は、再生セッション中のすべてのドロップフレームの合計として計算されます。この値は、(l:stream:dropped_frames)の最後の値から取得されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> ハートビート：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ドロップフレーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>droppedFrameCount) </li> <li> **データフィード：**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>droppedFrameCount) </li> </ul> |



### バッファーイベント

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：2 </li><li> **説明：バ**<br/>ッファーイベントの数。 この指標は、再生セッション中に発生した複数のバッファー状態の総数として計算されます。プレーヤーが他の状態（再生、一時停止など）からバッファー状態に移行した回数となります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>バッファーイベント </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bufferCount) </li> <li> **データフィード：**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bufferCount) </li> </ul> |



### 合計バッファー時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK バージョン：** </li> <li> ****<br/> サンプル値：30 </li><li> **説明：バ**<br/>ッファリングに費やした合計時間（秒）。 この値は、再生セッション中に発生したすべてのバッファーイベントの時間の合計として計算されます。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> ハートビート：(l:event:duration) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>合計バッファー時間 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bufferTime) </li> <li> **データフィード：**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bufferTime) </li> </ul> |



### ビットレート変更

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.qoe.bitrateChange </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：3 </li><li> **説明：ビ**<br/>ットレート変更の数（整数）。 この値は、再生セッション中に発生したすべてのビットレート変更イベントの合計として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビットレート変更 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **データフィード：**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bitrateChangeCount) </li> </ul> |



### エラー／エラーイベント

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 </li><li> **説明：発**<br/>生したエラーの数（整数）。 この値は、再生セッション中に発生したすべてのエラーイベントの合計として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>errorCount) </li> <li> **データフィード：**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>errorCount) </li> </ul> |



### プレーヤー SDK のエラー ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値：**<br/> </li><li> **説明：プ**<br/>レイヤーSDKによって生成された一意のエラーID。 お客様は、実装時に提供されたエラー API を使用してエラーコードや ID を指定する必要があります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> データフィード：videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>playerSdkErrors) </li> </ul> |



### 外部エラー ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値：**<br/> </li><li> **説明：**<br/>CDNエラーなど、任意の外部ソースからの一意のエラーID。 お客様は、実装時に提供されたエラー API を使用してエラーコードや ID を指定する必要があります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> データフィード：videoqoeextnererrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>externalErrors) </li> </ul> |



### メディア SDK のエラー ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値：**<br/> </li><li> **説明：再**<br/>生中にMedia SDKによって生成された一意のエラーID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エラー </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>mediaSdkErrors) </li> <li> **データフィード：**<br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>mediaSdkErrors) </li> </ul> |




### セッション終了 {#session-end}

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 2.1 </li> <li> ****<br/> サンプル値：end </li><li> **説明：endイ**<br/>ベントは、SDKがバックエンドに対してclose呼び出しを送信していることを意味します。 バックエンドがこのイベントを受信すると、そのビデオのセッションを終了し、それ以上処理をおこないません。<br/>メディアが100%に完了した場合は、「コンテンツ完了」の後に関連情報を `s:event:type=complete.` 送 [信する必要があります](audio-video-parameters.md#content-complete) 。 </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> ****<br/> ハートビート：(s:event:type=end) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager：**<br/> </li> </ul> |



## 品質指標 {#quality-metrics}

### 開始時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：30,000 </li><li> **説明：QoSObject**<br/>を使用して設定しない場合、この値のデフォルトは0です。 この値はミリ秒単位で設定します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> ハートビート：(l:stream:startup_time) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>開始時間 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>timeToStart) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>timeToStart) </li> </ul> |



### バッファーイベント

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：2 </li><li> **説明：バ**<br/>ッファーイベントの数（整数）。 この指標は、再生セッション中に発生したバッファーイベントの総数として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>バッファーイベント </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bufferCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bufferCount) </li> </ul> |



### 合計バッファー時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：15 </li><li> **説明：**<br/>バッファリングに費やした合計時間（秒）整数)。 この値は、再生セッション中に発生したすべてのバッファーイベントの時間の合計として計算されます。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> ハートビート：(l:event:duration) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>合計バッファー時間 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bufferTime) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bufferTime) </li> </ul> |



### ビットレート変更

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>イベント </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値："3" </li><li> **説明：ビ**<br/>ットレートの変更数。 この値は、再生セッション中に発生したすべてのビットレート変更イベントの合計として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ビットレート変更 </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bitrateChangeCount) </li> </ul> |



### エラー

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 </li><li> **説明：発**<br/>生したエラーの数（整数）。 この値は、再生セッション中に発生したすべてのエラーイベントの合計として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>エラーイベント </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>errorCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>errorCount) </li> </ul> |



### ドロップフレーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 </li><li> **説明：ド**<br/>ロップフレームの数（整数）。 この値は、再生セッション中のすべてのドロップフレームの合計として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> ハートビート：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ドロップフレーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>droppedFrameCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>droppedFrameCount) </li> </ul> |



### 開始前にドロップ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：ユ**<br/>ーザーがビデオを開始する前に終了した回数。 この指標は、広告とは無関係に、コンテンツがレンダリングされなかった場合に 1 に設定されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>開始前にドロップ </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>dropBeforeStart) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### バッファーの影響を受けたストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：バッフ**<br/>ァリングの影響を受けたストリームの数。 この指標は、再生セッション中に少なくとも 1 つのバッファーイベントが発生した場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>buffer) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>バッファーの影響を受けたストリーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>buffer) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### ビットレート変更の影響を受けたストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：ビ**<br/>ットレート変更が発生したストリームの数。 この指標は、再生セッション中に少なくとも 1 つのビットレート変更イベントが発生した場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> ****<br/> レポート名：ビットレート変更の影響を受けたストリーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bitrateChange) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### 平均ビットレート

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：3200 </li><li> **説明：平**<br/>均ビットレート（kbps、整数）。 この指標は、再生セッション中に発生した再生時間に関連するすべてのビットレート値の加重平均として計算されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> ハートビート：(l:stream:bitrate) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>平均ビットレート </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>bitrateAverage) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>bitrateAverage) </li> </ul> |



### エラーの影響を受けたストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：**<br/>エラーイベントが発生したストリームの数(例：再生セッション中に呼び出さ `trackError` れ、ハートビート呼び出しが生 `type=error` 成された)。 </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>エラー) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>エラーの影響を受けたストリーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>エラー) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>エラー) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### ドロップフレームの影響を受けたストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：フ**<br/>レームがドロップされたストリームの数。 この指標は、再生セッション中に少なくとも 1 つのフレームがドロップした場合にのみ、1 に設定されます。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> ハートビート：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>ドロップフレームの影響を受けたストリーム </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>droppedFrames) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### 停止の影響を受けたストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：停**<br/>止したイベントが発生したストリームの数。 この指標は、再生セッション中に少なくとも 1 回、停止が発生した場合にのみ 1 に設定されます。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stall) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>stall) </li> </ul> |



>[!IMPORTANT]
>このイベントが設定されている場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。

### 停止イベント

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> ****<br/> サンプル値："3" </li><li> **説明：**<br/>再生セッション中に再生が停止した回数。 レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallCount) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>stallCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>stallCount) </li> </ul> |



### 合計停止時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5 以上 </li> <li> ****<br/> サンプル値：12 </li><li> **説明：**<br/>合計時間（秒）integer)再生セッション中に停止された再生。 レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallTime) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.qoe.<br/>stallTime) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe<br/>stallTime) </li> </ul> |



## 関連API {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* JavaScript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

