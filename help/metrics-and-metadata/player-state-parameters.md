---
title: プレイヤーの状態パラメーター
description: このトピックでは、プレイヤー状態の追跡パラメーターについて説明します。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 73c579ec013d15ab47faa936cca1297f7052a8fb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 26%

---


# プレイヤーの状態パラメーター{#player-state-parameters}

このトピックでは、ソリューション変数を介してアドビが収集するプレーヤー状態データのリストを紹介します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *送信タイミング* - データが送信されるタイミング。*メディア開始*&#x200B;の場合はメディアの開始時に分析の呼び出しが送信され、*広告開始*&#x200B;の場合は広告の開始時に分析の呼び出しが送信されます。*終了*&#x200B;の場合は、メディアセッションや広告、チャプターなどの終了時に、コンパイル済みの分析の呼び出しがハートビートサーバーから分析サーバーに直接送信されます。終了の呼び出しは、ネットワークパケットの呼び出しでは利用できません。
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

>[!IMPORTANT]
>
>以下にリストされている変数で、レポート／予約変数に「分類」と説明されている変数の分類名を変更しないでください。\
>メディア分類は、レポートスイートでメディアトラッキングが有効にされる際に定義されます。アドビは新しいプロパティを追加することがありますが、その場合、新しいメディアプロパティにアクセスするには、レポートスイートを再有効化する必要があります。更新処理の際に、アドビは、変数の名前をチェックすることで、分類が有効にされているかどうかを判別します。見つからない変数名がある場合、アドビは、分類を再追加します。

## プレイヤー状態プロパティ {#player-state-properties}

プレイヤー状態追跡機能は、オーディオまたはビデオストリームに付加することができる。 標準化されたプレーヤー状態トラッキング指標は、ソリューション変数として保存されます。 標準の状態は次のとおりです。 fullScreen、mute、closeCaption、pictureInPicture、inFocus。

### フルスクリーンプロパティ

#### 全画面表示の影響を受けるストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明：フルスクリーンの影響を受けるストリームの数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要**<br/> ：このイベントを設定した場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.fullscreen.set<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **フルスクリーンの影響を受けるレポート名&#x200B;**<br/>・ストリーム</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.fullscreen.set<br/> </li> <li> **データフィード&#x200B;**<br/>videostatefullscreen</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.a.media.states.fullscreen.set</li> </ul> |

#### 全画面表示回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明：フルスクリーンが表示された回数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：このイベントを設定した場合、カウントは、ビデオがフルスクリーン状態だった回数と等しくなります。 このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.fullscreen.count<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>：フルスクリーン数</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.fullscreen.count<br/> </li> <li> **データフィード&#x200B;**<br/>videostatefullscreencount</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.fullscreen.count</li> </ul> |



#### 全画面表示時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明フルスクリーンが表示された時間の長さ。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：このイベントを設定した場合、時間はビデオがフルスクリーン状態だった時間と等しくなります。 このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.fullscreen.time<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>Full Screen Total Duration</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.fullscreen.time<br/> </li> <li> **データフィード&#x200B;**<br/>videostatefullscreentime</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.fullscreen.time</li> </ul> |


### クローズドキャプションのプロパティ

#### クローズドキャプションの影響を受けるストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明クローズドキャプションの影響を受けたストリームの数。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要**<br/> ：このイベントを設定した場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.closedcaptioning.set<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **クローズドキャプションの影響を受けるレポート名&#x200B;**<br/>・ストリーム</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.closedcaptioning.set<br/> </li> <li> **データフィード&#x200B;**<br/>videostateclosedcaption</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.a.media.states.closedcaptioning.set</li> </ul> |


#### クローズドキャプション回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明クローズドキャプションが表示された回数。 This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **重要&#x200B;**<br/>このイベントを設定した場合、カウントは、ビデオがクローズドキャプション状態だった回数と等しくなります。 このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>C19<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>/クローズドキャプションカウント</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.closedcaptioning.count<br/> </li> <li> **データフィード&#x200B;**<br/>videostateclosedcaptioningcount</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.closedcaptioning.count</li> </ul> |


#### クローズドキャプション時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明クローズドキャプションが表示された時間の長さ。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：このイベントを設定した場合、時間は、ビデオがクローズドキャプション状態であった時間と等しくなります。 このイベントが設定されていない場合、値は送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.closedcaptioning.time<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>Closed Captioning Total Duration</li> <li> **Context Data **<br/>a.media.states.closedcaptioning.time<br/> </li> <li> **データフィード&#x200B;**<br/>videostateclosedcaptioningtime</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.closedcaptioning.time</li> </ul> |


### ミュートプロパティ

#### ミュートの影響を受けるストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明：ミュートの影響を受けたストリームの数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要**<br/> ：このイベントを設定した場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.mute.set<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **ミュートの影響を受けたレポート名&#x200B;**<br/>（ストリーム）</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.mute.set<br/> </li> <li> **データフィード&#x200B;**<br/>videostatemute</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.a.media.states.mute.set</li> </ul> |

#### ミュート回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明ミュートが表示された回数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：このイベントを設定した場合、カウントは、ビデオがミュート状態だった回数と等しくなります。 このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.mute.count<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>：ミュート数</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.mute.count<br/> </li> <li> **データフィード&#x200B;**<br/>videostatemutecount</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.mute.count</li> </ul> |

#### ミュート時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明ミュートが表示された時間の長さ。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：このイベントを設定した場合、時間はビデオがミュート状態にあった時間と等しくなります。 このイベントが設定されていない場合、値は送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.mute.time<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **レポート名&#x200B;**<br/>（ミュート）合計時間</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.mute.time<br/> </li> <li> **データフィード&#x200B;**<br/>videostatemutetime</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.mute.time</li> </ul> |


### 画像のプロパティの画像


#### ピクチャインピクチャの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明：ピクチャインピクチャの影響を受けたストリームの数。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：このイベントを設定した場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.pictureinpicture.set<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **ピクチャインピクチャの影響を受けるレポート名&#x200B;**<br/>・ストリーム</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.picture.set<br/> </li> <li> **データフィード&#x200B;**<br/>videostatepictureinpicture</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.a.media.states.pictureinpicture.set</li> </ul> |


#### 画像の数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明図の中の図が表示された回数です。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> このイベントを設定した場合、カウントは、ビデオがピクチャインピクチャ状態だった回数と等しくなります。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.pictureinpicture.count<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **画像数のレポート名&#x200B;**<br/>：画像</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.pictureinpicture.count<br/> </li> <li> **データフィード&#x200B;**<br/>videostatepictureinpicturecount</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.picture.count</li> </ul> |


#### 画像の合計時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明図の中の図が表示された時間の長さです。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> このイベントを設定した場合、時間は、ビデオがピクチャインピクチャ状態にあった時間と等しくなります。 このイベントが設定されていない場合、値は送信されません。   </li> </ul> | <ul> <li> **Adobe **<br/>Analyticsa.media.states.pictureinpicture.time<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **画像内のレポート名&#x200B;**<br/>Picture （画像合計時間）</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.picture.time<br/> </li> <li> **データフィード&#x200B;**<br/>videostatepictureinpicturetime</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.pictureinpicture.time</li> </ul> |


### フォーカス内のプロパティ

#### フォーカス設定の影響を受けるストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明フォーカスが与えられたストリームの数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> ：このイベントを設定した場合、可能な値はTRUEのみです。 このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.infocus.set<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **フォーカスの影響を受けたレポート名&#x200B;**<br/>・ストリーム</li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.infocus.set<br/> </li> <li> **データフィード&#x200B;**<br/>videostateinfocus</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.a.media.states.infocus.set</li> </ul> |


#### フォーカス設定回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明フォーカスが表示された回数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要&#x200B;**<br/>このイベントを設定した場合、カウントは、ビデオがフォーカス状態だった回数と等しくなります。 このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.infocus.count<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **フォーカス数のレポート名&#x200B;**<br/></li> <li> **コンテキストデータ&#x200B;**<br/>a.media.states.infocus.count<br/> </li> <li> **データフィード&#x200B;**<br/>videostateinfocuscount</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.infocus.count</li> </ul> |


#### フォーカス設定時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDKキー&#x200B;**<br/>：自動的に設定</li> <li> **APIキー&#x200B;**<br/>該当なし</li> <li> **必須&#x200B;**<br/>No</li> <li> **タイプ&#x200B;**<br/>番号</li> <li> **メディアを閉じると共に送信&#x200B;**<br/></li> <li> **最小のSDK Version **<br/>3.0</li> <li> **サンプル値&#x200B;**<br/>TRUE</li><li> ****<br/>説明フォーカスが表示された時間。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> このイベントを設定した場合、時間はビデオがフォーカス状態にあった時間と等しくなります。 このイベントが設定されていない場合、値は送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>a.media.states.infocus.time<br/></li> <li> **ハートビート&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **使用可能&#x200B;**<br/>Yes</li> <li> **予約変数&#x200B;**<br/>イベント</li> <li> **フォーカスされたレポート名&#x200B;**<br/>（合計期間）</li> <li> **Context Data **<br/>a.media.states.infocus.time<br/> </li> <li> **データフィード&#x200B;**<br/>videostateinfocustime</li> <li> **オーディエンスマネージャ&#x200B;**<br/>c_contextdata.media.states.infocus.time</li> </ul> |

## XDM IDのプロパティリスト

Analyticsに保存されたデータはどのような目的でも使用でき、プレーヤー状態指標は、XDMを使用してAdobe Experience Platformにインポートし、Customer Jeurney Analyticsで使用できます。

| プレイヤー状態プロパティ | マッピング |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## 関連する API {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
