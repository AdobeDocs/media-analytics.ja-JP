---
title: プレーヤーステートパラメーター
description: '"フルスクリーン、クローズドキャプション、ミュート、およびピクチャーインピクチャーのプロパティのプレーヤーステートトラッキングパラメーターについて説明します。"'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: '"Media Analytics，変数"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 99%

---

# プレーヤーステートパラメーター{#player-state-parameters}

このトピックでは、ソリューション変数を介してアドビが収集するプレーヤーステートデータのリストを紹介します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *送信タイミング* - データが送信されるタイミング。*メディア開始*&#x200B;の場合はメディアの開始時に分析の呼び出しが送信され、*広告開始*&#x200B;の場合は広告の開始時に分析の呼び出しが送信されます。*終了*&#x200B;の場合は、メディアセッションや広告、チャプターなどの終了時に、コンパイル済みの分析の呼び出しがハートビートサーバーから分析サーバーに直接送信されます。終了の呼び出しは、ネットワークパケットの呼び出しでは利用できません。
   * *最小のSDK のバージョン* - パラメーターにアクセスするのに必要な SDK のバージョン。
   * *値の例* - 変数の一般的な利用方法の例。
* **ネットワークパラメーター：** Adobe Analytics またはハートビートサーバーに渡される値。この列には、Adobe Media SDK によって生成されるネットワーク呼び出しに含まれるパラメーターの名前が示されています。
* **レポート：**&#x200B;ビデオデータの確認方法と分析方法に関する詳細。
   * *利用可能* - デフォルトでもデータをレポートで確認できる場合は&#x200B;*可*、カスタム設定が必要な場合は&#x200B;*カスタム*。
   * *予約変数* - 予約変数で取得されるデータの形式（イベント、eVar、prop または分類）。
   * *レポート名* - Adobe Aanlytics の変数のレポート名。
   * *コンテキストデータ* - レポートサーバーに渡され、処理ルールで使用される Adobe Analytics のコンテキストデータの名前。
   * *データフィード* - クリックストリームまたはライブストリームデータフィード内の変数の列の名前。
   * *Audience Manager* - Adobe Audience Manager 内の特性名。

>[!IMPORTANT]
>
>以下にリストされている変数で、レポート／予約変数に「分類」と説明されている変数の分類名を変更しないでください。\
>メディア分類は、レポートスイートでメディアトラッキングが有効にされる際に定義されます。アドビは新しいプロパティを追加することがありますが、その場合、新しいメディアプロパティにアクセスするには、レポートスイートを再有効化する必要があります。更新処理の際に、アドビは、変数の名前をチェックすることで、分類が有効にされているかどうかを判別します。見つからない変数名がある場合、アドビは、分類を再追加します。

## プレーヤーステートプロパティ {#player-state-properties}

プレーヤーステートトラッキング機能は、オーディオまたはビデオストリームにアタッチできます。標準化されたプレーヤーステートトラッキング指標は、ソリューション変数として保存されます。標準のステートは、フルスクリーン、ミュート、クローズドキャプション、ピクチャーインピクチャー、フォーカス設定です。

### フルスクリーンプロパティ

#### 全画面表示の影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;フルスクリーンの影響を受けたストリームの数。この指標は、再生セッション中にフルスクリーンステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.fullscreen.set<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フルスクリーンの影響を受けたストリーム </li> <li> **コンテキストデータ**<br/> a.media.states.fullscreen.set<br/> </li> <li> **データフィード**<br/> videostatefullscreen </li> <li> **Audience Manager：**<br/> c_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### フルスクリーンの回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;フルスクリーンが表示された回数。この指標は、再生セッション中にフルスクリーンステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要：**<br/>&#x200B;このイベントを設定した場合、カウントは、ビデオがフルスクリーンステートだった回数と等しくなります。このイベントを設定しない場合は、値が送信されません。</li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.fullscreen.count<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フルスクリーンの回数 </li> <li> **コンテキストデータ**<br/> a.media.states.fullscreen.count<br/> </li> <li> **データフィード**<br/> videostatefullscreencount </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.fullscreen.count </li> </ul> |



#### 全画面表示時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;フルスクリーンが表示された時間の長さ。この指標は、再生セッション中にフルスクリーンステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要：**<br/>&#x200B;このイベントを設定した場合、時間はビデオがフルスクリーンステートだった期間と等しくなります。このイベントを設定しない場合は、値が送信されません。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.fullscreen.time<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フルスクリーンの時間合計 </li> <li> **コンテキストデータ**<br/> a.media.states.fullscreen.time<br/> </li> <li> **データフィード**<br/> videostatefullscreentime </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.fullscreen.time </li> </ul> |


### クローズドキャプションのプロパティ

#### クローズドキャプションの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;クローズドキャプションの影響を受けたストリームの数。この指標は、再生セッション中にクローズドキャプションステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.closedcaptioning.set<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;クローズドキャプションの影響を受けたストリーム </li> <li> **コンテキストデータ**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **データフィード**<br/> videostateclosedcaptioning </li> <li> **Audience Manager：**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### クローズドキャプションの回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;クローズドキャプションが表示された回数。この指標は、再生セッション中にクローズドキャプションステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>&#x200B;このイベントを設定した場合、カウントは、ビデオがクローズドキャプションステートだった回数と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.count<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;クローズドキャプションの回数 </li> <li> **コンテキストデータ**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **データフィード**<br/> videostateclosedcaptioningcount </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### クローズドキャプション時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;クローズドキャプションが表示された時間の長さ。この指標は、再生セッション中にフルスクリーンステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要：**<br/>&#x200B;このイベントを設定した場合、時間は、ビデオがクローズドキャプションステートであった期間と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.closedcaptioning.time<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;クローズドキャプションの時間合計 </li> <li> **コンテキストデータ**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **データフィード**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.closedcaptioning.time </li> </ul> |


### ミュートのプロパティ

#### ミュートの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明：**<br/>&#x200B;ミュートの影響を受けたストリームの数。この指標は、再生セッション中にミュートステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.mute.set<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ミュートの影響を受けたストリーム </li> <li> **コンテキストデータ**<br/> a.media.states.mute.set<br/> </li> <li> **データフィード**<br/> videostatemute </li> <li> **Audience Manager：**<br/> c_contextdata.a.media.states.mute.set </li> </ul> |

#### ミュートの回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;ミュートが表示された回数。この指標は、再生セッション中にミュートステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要：**<br/>&#x200B;このイベントを設定した場合、カウントは、ビデオがミュートステートだった回数と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.mute.count<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ミュートの回数 </li> <li> **コンテキストデータ**<br/> a.media.states.mute.count<br/> </li> <li> **データフィード**<br/> videostatemutecount </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.mute.count </li> </ul> |

#### ミュート時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;ミュートが表示された時間の長さ。この指標は、再生セッション中にミュートステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要：**<br/>&#x200B;このイベントを設定した場合、時間はビデオがミュートステートにあった期間と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.mute.time<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ミュートの合計期間 </li> <li> **コンテキストデータ**<br/> a.media.states.mute.time<br/> </li> <li> **データフィード**<br/> videostatemutetime </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.mute.time </li> </ul> |


### ピクチャーインピクチャーのプロパティ


#### ピクチャーインピクチャーの影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明：**<br/>&#x200B;ピクチャーインピクチャーの影響を受けたストリームの数。この指標は、再生セッション中にピクチャーインピクチャー設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.pictureinpicture.set<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ピクチャーインピクチャーの影響を受けたストリーム </li> <li> **コンテキストデータ**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **データフィード**<br/> videostatepictureinpicture </li> <li> **Audience Manager：**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### ピクチャーインピクチャーの回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;ピクチャーインピクチャーが表示された回数。この指標は、再生セッション中にピクチャーインピクチャー設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定した場合、カウントは、ビデオがピクチャインピクチャステートだった回数と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.pictureinpicture.count<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ピクチャーインピクチャーの回数 </li> <li> **コンテキストデータ**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **データフィード**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.pictureinpicture.count </li> </ul> |


#### ピクチャーインピクチャーの時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;ピクチャーインピクチャーが表示された時間の長さ。この指標は、再生セッション中にピクチャーインピクチャー設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定した場合、時間は、ビデオがピクチャインピクチャステートにあった期間と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.pictureinpicture.time<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;ピクチャーインピクチャーの時間合計 </li> <li> **コンテキストデータ**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **データフィード**<br/> videostatepictureinpicturetime </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.pictureinpicture.time </li> </ul> |


### フォーカス設定のプロパティ

#### フォーカス設定の影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明：**<br/>&#x200B;フォーカス設定の影響を受けたストリームの数。この指標は、再生セッション中にフォーカス設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.infocus.set<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フォーカス設定の影響を受けたストリーム </li> <li> **コンテキストデータ**<br/> a.media.states.infocus.set<br/> </li> <li> **データフィード**<br/> videostateinfocus </li> <li> **Audience Manager：**<br/> c_contextdata.a.media.states.infocus.set </li> </ul> |


#### フォーカス設定回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;フォーカス設定が表示された回数。この指標は、再生セッション中にフォーカス設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>&#x200B;このイベントを設定した場合、カウントは、ビデオがフォーカス設定ステートだった回数と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.infocus.count<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フォーカス設定の回数 </li> <li> **コンテキストデータ**<br/> a.media.states.infocus.count<br/> </li> <li> **データフィード**<br/> videostateinfocuscount </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.infocus.count </li> </ul> |


#### フォーカス設定時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー**<br/>&#x200B;自動設定  </li> <li> **API キー**<br/>&#x200B;なし </li> <li> **必須**<br/>&#x200B;いいえ </li> <li> **型**<br/>&#x200B;数値 </li> <li> **送信タイミング**<br/>&#x200B;メディアの終了 </li> <li> **最小のSDK のバージョン**<br/> 3.0</li> <li> **値の例**<br/> TRUE </li><li> **説明**<br/>&#x200B;フォーカス設定が表示された時間の長さ。この指標は、再生セッション中にフォーカス設定ステートが 1 回以上発生した場合にのみ、1 に設定されます。<br/> **重要**<br/>このイベントを設定した場合、時間はビデオがフォーカス設定ステートにあった期間と等しくなります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> a.media.states.infocus.time<br/></li> <li> **ハートビート**<br/>&#x200B;該当なし </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名**<br/>&#x200B;フォーカス設定の時間合計 </li> <li> **コンテキストデータ**<br/> a.media.states.infocus.time<br/> </li> <li> **データフィード**<br/> videostateinfocustime </li> <li> **Audience Manager：**<br/> c_contextdata.media.states.infocus.time </li> </ul> |

## XDM ID のプロパティリスト

Analytics に保存されたデータはどのような目的でも使用でき、プレーヤーステート指標は XDM を使用して Adobe Experience Platform に読み込み、Customer Journey Analytics で使用することができます。

| プレーヤーステートのプロパティ | マッピング |
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
