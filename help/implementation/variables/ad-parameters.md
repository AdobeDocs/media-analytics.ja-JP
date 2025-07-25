---
title: '広告パラメーター '
description: 広告ビデオデータの実装、ネットワーク、レポート変数などの広告パラメーターについて説明します。
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 89%

---

# 広告パラメーター {#ad-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するビデオ広告データのリストを示します。

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
   * *Audience Manager* - Adobe Audience Manager 内の特性名。

>[!IMPORTANT]
>
>以下にリストされている変数で、レポート／予約変数に「分類」と説明されている変数の分類名を変更しないでください
>&#x200B;>。
>&#x200B;>メディア分類は、レポートスイートでメディアトラッキングが有効にされる際に定義されます
>&#x200B;>。アドビは新しいプロパティを追加することがありますが、その場合、
>&#x200B;>新しいメディアプロパティにアクセスするには、レポートスイートを再有効化する必要があります
>&#x200B;>。更新処理の際に、アドビは、変数の名前をチェックすることで、
>&#x200B;>分類が有効にされているかどうかを判別します。見つからない
>&#x200B;>変数名がある場合、アドビは、分類を再追加します。

## 広告ビデオデータ {#ad-video-data}

### 広告 ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.id </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可  </li> <li> **値の例：**<br/> 2125 </li><li> **説明：**<br/>&#x200B;広告の ID。（整数と文字の組み合わせ）。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>name） </li> <li> **ハートビート：**<br/> （<code>s:asset:ad_id</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;訪問時 </li> <li> **レポート名：**<br/>&#x200B;広告 </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>name） </li> <li> **データフィード：**<br/> videoad </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.name） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference_id </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.name </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### ポッド位置の広告

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.podPosition </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 1 </li><li> **説明：**<br/>&#x200B;親広告ブレーク内の広告の位置（インデックス）。最初の広告のインデックスは 0、2 番目の広告のインデックスは 1（以下同様）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>podPosition） </li> <li> **ハートビート：**<br/> （<code>s:asset:pod_position</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;ポッド位置の広告 </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>podPosition） </li> <li> **データフィード：**<br/> videoadinpod </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.podPosition） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetViewDetails.index </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.podPosition </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.podPosition </li> </ul> |



### 広告の長さ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.length </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/> 「15」  </li><li> **説明：**<br/>&#x200B;ビデオ広告の長さ（秒）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>length） </li> <li> **ハートビート：**<br/> （<code>l:asset:ad_length</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar および分類 </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;広告の長さおよび広告の長さ（変数） </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>length） </li> <li> **データフィード：**<br/> videoadlength </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.length） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference<br/>_xmpDM.duration </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.length </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### 広告プレーヤー名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.playerName </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 「Freewheel」 </li><li> **説明：**<br/>&#x200B;広告のレンダリングをおこなうプレーヤーの名前。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>playerName） </li> <li> **ハートビート：**<br/> （<code>s:sp:player_name</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;広告プレーヤー名 </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>playerName） </li> <li> **データフィード：**<br/> videoadplayername </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.playerName） </li> <li> **XDM フィールドパス：** （非推奨） <br/> advertising.adAssetViewDetails.playerName </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### 広告ブレーク名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.podFriendlyName </li> <li> **必須：**<br/> SDK：はい、API：いいえ。 </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 「pre-roll」 </li><li> **説明：**<br/>&#x200B;広告ブレークのわかりやすい名前。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>podFriendlyName） </li> <li> **ハートビート：**<br/> （<code>s:asset:pod_name</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;ポッド名 </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>podFriendlyName） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.podFriendlyName） </li> <li> **XDM フィールドパス：** （非推奨） <br/> advertising.adAssetViewDetails.<br/>adBreak._dc.title </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### 広告ブレークインデックス

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.podIndex </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/> </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 1 </li><li> **説明：**<br/>&#x200B;コンテンツ内の広告ブレークのインデックス（1 から開始）。このプロパティは、メディア SDK でポッド ID を生成するために **のみ** 使用します。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;不可 </li> <li> **予約変数：**<br/>&#x200B;なし </li> <li> **レポート名：**<br/>&#x200B;なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/> </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetViewDetails.index </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### 広告ブレークの位置

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.podSecond </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 90 </li><li> **説明：**<br/>&#x200B;コンテンツ内の広告ブレークのオフセット（秒）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>podSecond） </li> <li> **ハートビート：**<br/> （<code>l:asset:pod_offset</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;ポッド位置 </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>podSecond） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.podSecond） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetViewDetails.adBreak。<br/>offset </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingPodDetails.<br/>offset </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingPodDetails.<br/>offset </li> </ul> |



### 広告ブレーク ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定 </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>pod） </li> <li> **ハートビート：**<br/> （<code>s:asset:pod_id</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;広告ポッド </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>pod） </li> <li> **データフィード：**<br/> videoadpod </li> <li> **Audience Manager：**<br/> </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetViewDetails.adBreak。_id </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### 広告名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/> media.ad.name </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/> 「Ford F-150」 </li><li> **説明：**<br/>&#x200B;広告のわかりやすい名前。レポートでは、「広告名」が分類、「広告名（変数）」が eVar です。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>friendlyName） </li> <li> **ハートビート：**<br/> （<code>s:asset:ad_name</code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar および分類 </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;広告名および広告名（変数） </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>friendlyName） </li> <li> **データフィード：**<br/> videoadname </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.friendlyName） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference_dc.title </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## 標準の広告メタデータ {#standard-ad-metadata}

### 広告主

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> ADVERTISER </li> <li> **API キー：**<br/> media.ad.advertiser </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;広告で商品が取り上げられる会社またはブランド。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>advertiser） </li> <li> **ハートビート：**<br/> （<code>s:meta:</code><br/>a.media.ad.advertiser） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/> <i>広告主 </i> </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>advertiser） </li> <li> **データフィード：**<br/> videoadadadvertiser </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.advertiser） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.advertiser </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### キャンペーン ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> CAMPAIGN_ID </li> <li> **API キー：**<br/> media.ad.campaignId </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/> 整数、または名前（文字列）。  </li><li> **説明：**<br/>&#x200B;広告キャンペーンの ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>campaign） </li> <li> **ハートビート：**<br/> （<code>s:meta:</code><br/>a.media.ad.campaign） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/> <i>キャンペーン ID </i> </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>campaign） </li> <li> **データフィード：**<br/> videoadcampaign </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.campaign） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.campaign </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### クリエイティブ ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> CREATIVE_ID </li> <li> **API キー：**<br/> media.ad.creativeId </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/> 整数、または名前（文字列）。  </li><li> **説明：**<br/>&#x200B;広告クリエイティブの ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>creative） </li> <li> **ハートビート：**<br/> （<code>s:meta:</code><br/>a.media.ad.creative） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/> <i>クリエイティブ ID </i> </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>creative） </li> <li> **データフィード：**<br/> adclassificationcreative </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.creative） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.creativeID </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### サイト ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> SITE_ID </li> <li> **API キー：**<br/> media.ad.siteId </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;広告サイトの ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>site） </li> <li> **ハートビート：**<br/> （<code>s:meta:</code><br/>a.media.ad.site） </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタムの処理ルールを使用</i> </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;カスタム </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>site） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.site） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.siteID </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### クリエイティブ URL

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> CREATIVE_URL </li> <li> **API キー：**<br/> media.ad.creativeURL </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;広告クリエイティブの URL。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>creativeURL） </li> <li> **ハートビート：**<br/> （<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL） </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタムの処理ルールを使用</i> </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;カスタム </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>creativeURL） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.creativeURL） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.creativeURL </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### プレースメント ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/> PLACEMENT_ID </li> <li> **API キー：**<br/> media.ad.placementId </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;広告のプレースメント ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>placement） </li> <li> **ハートビート：**<br/> （<code>s:meta:</code><br/>a.media.ad.placement） </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタムの処理ルールを使用</i> </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;カスタム </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>placement） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.placement） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.adAssetReference.placementID </li> <li> **コレクション XDM フィールドのパス：**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## 広告指標 {#ad-metrics}

### 広告開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定 </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告開始 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> TRUE </li><li> **説明：**<br/>&#x200B;ビデオ広告の開始数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>view） </li> <li> **ハートビート：**<br/> （<code>s:event:type=start</code>） <br/> （<code>s:asset:type=ad<code>） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;広告開始 </li> <li> **データフィード：**<br/> videoadstart </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>view） </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.view） </li> <li> **XDM フィールドパス：** （非推奨） <br/>advertising.impressions.value > 0 => &quot;TRUE&quot; </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### 広告完了

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定 </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> TRUE </li><li> **説明：**<br/>&#x200B;ビデオ広告の完了数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>complete） </li> <li> **ハートビート：**<br/> （<code>s:event:type=complete</code>） <br/> （<code>s:asset:type=ad</code>）  </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;広告完了 </li> <li> **データフィード：**<br/> videoadcomplete </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>complete） </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.complete） </li> <li> **XDM フィールドパス：** （非推奨） <br/> advertising.completes.value > 0 => &quot;TRUE&quot; </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### 広告滞在時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定 </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/> 15 </li><li> **説明：**<br/>&#x200B;広告の合計視聴時間（再生秒数）。値は時間形式（<code>HH:MM:SS</code>Analysis Workspace）に設定する必要があります。 データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.ad.<br/>timePlayed） </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;広告滞在時間 </li> <li> **データフィード：**<br/> videoadtime </li> <li> **コンテキストデータ：**<br/>（a.media.ad.<br/>timePlayed） </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.ad.timePlayed） </li> <li> **XDM フィールドパス：** （非推奨） <br/> advertising.timePlayed.value </li> <li> **レポート XDM フィールドのパス：**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



## 関連する API {#section_Related_APIs}

### createAdObject API：

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API：

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API：

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
