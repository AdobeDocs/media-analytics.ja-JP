---
title: 広告パラメーター
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 広告パラメーター{#ad-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するビデオ広告データのリストを示します。

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

>[!IMPORTANT]
>
>以下に示す変数の分類名は変更しないでください。
>「レポート/予約変数」で「分類」として説明されています。
>メディア分類は、レポートスイートがメディアに対して有効になっている場合に定義されます
>トラッキング. アドビは、新しいプロパティを随時追加し、その場合は、
>顧客が新しいメディアにアクセスするには、レポートスイートを再度有効にする必要があります。
>プロパティ。 更新プロセス中に、
>分類を有効にするには、変数の名前を確認します。 いずれかの
>見つからない場合は、見つからないものが再度追加されます。

## 広告ビデオデータ {#ad-video-data}

### 広告 ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.id </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可  </li> <li> ****<br/> サンプル値："2125" </li><li> **説明：**<br/>広告のID。 （整数と文字の組み合わせ）。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>name) </li> <li> ****<br/> ハートビート：(s:asset:ad_id) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>広告 </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>name) </li> <li> **データフィード：**<br/>videoad </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### ポッド位置の広告

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podPosition </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 </li><li> **説明：親**<br/>広告ブレーク内の広告の位置（インデックス）。 最初の広告のインデックスは 0、2 番目の広告のインデックスは 1（以下同様）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podPosition) </li> <li> ****<br/> ハートビート：(s:asset:pod_position) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ポッド位置の広告 </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>podPosition) </li> <li> **データフィード：**<br/>videoadinpod </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 広告の長さ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> ****<br/> サンプル値："15"  </li><li> **説明：ビ**<br/>デオ広告の長さ（秒）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>length) </li> <li> ****<br/> ハートビート：(l:asset:ad_length) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar および分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告の長さおよび広告の長さ（変数） </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>length) </li> <li> **データフィード：**<br/>videoadlength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### 広告プレーヤー名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.playerName </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：「フリーホイール」 </li><li> **説明：広**<br/>告のレンダリングを担当するプレーヤーの名前。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>playerName) </li> <li> ****<br/> ハートビート：(s:sp:player_name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告プレーヤー名 </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>playerName) </li> <li> **データフィード：**<br/>videoadplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 広告ブレーク名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podFriendlyName </li> <li> ****<br/> 必須：SDK:そうだ。API:いいえ。 </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：「プリロール」 </li><li> **説明：**<br/>広告の時間のわかりやすい名前。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> ハートビート：(s:asset:pod_name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>ポッド名 </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>podFriendlyName) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 広告ブレークインデックス

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podPosition </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/> </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 </li><li> **説明：1**<br/>から始まるコンテンツ内の広告ブレークのインデックス。 このプロパティは、メディア SDK でポッド ID を生成するために&#x200B;**のみ**&#x200B;使用します。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>不可 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 広告ブレークの位置

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podSecond </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：90 </li><li> **説明：コ**<br/>ンテンツ内の広告の時間のオフセット（秒）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>podSecond) </li> <li> ****<br/> ハートビート：(l:asset:pod_offset) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>ポッド位置 </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>podSecond) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 広告ブレーク ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>ポッド) </li> <li> ****<br/> ハートビート：(s:asset:pod_id) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告ポッド </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>ポッド) </li> <li> **データフィード：**<br/>videoadpod </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 広告名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> ****<br/> サンプル値：「Ford F-150」 </li><li> **説明：広**<br/>告のわかりやすい名前。  レポートでは、「広告名」が分類、「広告名（変数）」が eVar です。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>friendlyName) </li> <li> ****<br/> ハートビート：(s:asset:ad_name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar および分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告名および広告名（変数） </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>friendlyName) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 標準の広告メタデータ {#standard-ad-metadata}

### 広告主

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ADVERTISER </li> <li> **API キー：**<br/>media.ad.advertiser </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値：**<br/> </li><li> **説明：**<br/>広告で製品が取り上げられる会社/ブランド。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>advertiser) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>広告主 </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>advertiser) </li> <li> **データフィード：**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### キャンペーン ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CAMPAIGN_ID </li> <li> **API キー：**<br/>media.ad.campaignId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：整数、または名前（文字列）。  </li><li> **説明：広**<br/>告キャンペーンのID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>campaign) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>キャンペーン ID </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>campaign) </li> <li> **データフィード：**<br/>videocampaign </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### クリエイティブ ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CREATIVE_ID </li> <li> **API キー：**<br/>media.ad.creativeId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：整数、または名前（文字列）。  </li><li> **説明：広**<br/>告クリエイティブのID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>creative) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>クリエイティブ ID </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>creative) </li> <li> **データフィード：**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### サイト ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SITE_ID </li> <li> **API キー：**<br/>media.ad.siteId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値：**<br/> </li><li> **説明：**<br/>広告サイトのID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>site) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>site) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### クリエイティブ URL

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CREATIVE_URL </li> <li> **API キー：**<br/>media.ad.creativeURL </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値：**<br/> </li><li> **説明：広**<br/>告クリエイティブのURL。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>creativeURL) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>creativeURL) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### プレースメント ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>PLACEMENT_ID </li> <li> **API キー：**<br/>media.ad.placementId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値：**<br/> </li><li> **説明：**<br/>広告の配置ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>placement) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **利用可能：**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>placement) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 広告指標 {#ad-metrics}

### 広告開始

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：開**<br/>始したビデオ広告の数。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>view) </li> <li> ****<br/> ハートビート： (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告開始 </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>view) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### 広告完了

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：**<br/>ビデオ広告完了の数。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>complete) </li> <li> ****<br/> ハートビート：(s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告完了 </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>complete) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 広告滞在時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：15 </li><li> **説明：**<br/>広告の視聴に費やした合計時間（秒単位、再生秒数）。  Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ad.<br/>timePlayed) </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告滞在時間 </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> コンテキストデータ：(a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## 関連API {#section_Related_APIs}

### createAdObject API:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

