---
seo-title: 広告パラメーター
title: 広告パラメーター
uuid: 92cd7f97- bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# 広告パラメーター{#ad-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するビデオ広告データのリストを示します。

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

>[!IMPORTANT]
>
>以下に示す変数の分類名は変更しないでください
>を参照してください。
>メディア分類は、レポートスイートがメディアに対して有効になっているときに定義されます
>トラッキング. 今後、アドビは新しいプロパティを追加し、これが発生すると、
>顧客は、レポートスイートを再度有効にして、新しいメディアにアクセスする必要がある
>プロパティを参照してください。更新プロセスでは、
>分類を有効にすることができます。いずれかの場合
>見つからない場合、見つからないものが再度追加されます。

## 広告ビデオデータ {#section_hq3_nbv_51b}

### 広告 ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.id </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可  </li> <li> **サンプル値:**<br/> "2125" </li><li> **説明:**<br/>広告のID。（整数と文字の組み合わせ）。  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>name) </li> <li> **ハートビート:**<br/> （s:asset:ad_ id） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>広告 </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>name) </li> <li> **データフィード：**<br/>videoad </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### ポッド位置の広告

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podPosition </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1 </li><li> **説明:**<br/>親広告ブレーク内の広告の位置（インデックス）。最初の広告のインデックスは 0、2 番目の広告のインデックスは 1（以下同様）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>podPosition） </li> <li> **ハートビート:**<br/> （s:asset:pod_ position） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ポッド位置の広告 </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>podPosition） </li> <li> **データフィード：**<br/>videoadinpod </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 広告の長さ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **サンプル値:**<br/> "15"  </li><li> **説明:**<br/>ビデオ広告の長さ（秒単位）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>length) </li> <li> **ハートビート:**<br/> （l:asset:ad_ length） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar および分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告の長さおよび広告の長さ（変数） </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>length) </li> <li> **データフィード：**<br/>videoadlength </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### 広告プレーヤー名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.playerName </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 「フリーホイール」 </li><li> **説明:**<br/>広告のレンダリングを担当するプレーヤーの名前。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>playerName) </li> <li> **ハートビート:**<br/> （s:sp:player_ name） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告プレーヤー名 </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>playerName) </li> <li> **データフィード：**<br/>videoadplayername </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 広告ブレーク名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podFriendlyName </li> <li> **必須:**<br/> SDK:はい;API:いいえ。 </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> "pre- roll" </li><li> **説明:**<br/>広告ブレークのわかりやすい名前。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>PodFriendlyName） </li> <li> **ハートビート:**<br/> （s:asset:ポッド名） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>ポッド名 </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>PodFriendlyName） </li> <li> **データフィード：**<br/>videoadpod </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 広告ブレークインデックス

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podPosition </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/> </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1 </li><li> **説明:**<br/>コンテンツ内の広告ブレークのインデックス（1から始まる）。このプロパティは、メディア SDK でポッド ID を生成するために&#x200B;**のみ**&#x200B;使用します。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>不可 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>なし </li> <li> **コンテキストデータ：**<br/> </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 広告ブレークの位置

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.podSecond </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 90 </li><li> **説明:**<br/>コンテンツ内の広告ブレークのオフセット（秒単位）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>ポッド秒） </li> <li> **ハートビート:**<br/> （l:asset:pod_ offset） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>ポッド位置 </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>ポッド秒） </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 広告ブレーク ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>ポッド） </li> <li> **ハートビート:**<br/> （s:asset:pod_ id） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告ポッド </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>ポッド） </li> <li> **データフィード：**<br/>videoadpod </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 広告名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API キー：**<br/>media.ad.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **サンプル値:**<br/> 「フォードF-150" </li><li> **説明:**<br/>広告のわかりやすい名前。レポートでは、「広告名」が分類、「広告名（変数）」が eVar です。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>friendlyName） </li> <li> **ハートビート:**<br/> （s:asset:ad_ name） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar および分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>広告名および広告名（変数） </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>friendlyName） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 標準の広告メタデータ {#section_EFB805867916411E84DE1BA5A183D86A}

### 広告主

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ADVERTISER </li> <li> **API キー：**<br/>media.ad.advertiser </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>広告で製品が特集されている会社/ブランド。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>advertiser) </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.advertiser） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>広告主 </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>advertiser) </li> <li> **データフィード：**<br/>videoadvertiser </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### キャンペーン ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CAMPAIGN_ID </li> <li> **API キー：**<br/>media.ad.campaignId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> 整数（文字列）。  </li><li> **説明:**<br/>広告キャンペーンのID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>campaign) </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.campaign） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>キャンペーン ID </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>campaign) </li> <li> **データフィード：**<br/>videocampaign </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### クリエイティブ ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CREATIVE_ID </li> <li> **API キー：**<br/>media.ad.creativeId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> 整数（文字列）。  </li><li> **説明:**<br/>広告クリエイティブのID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>creative) </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.creative） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i>クリエイティブ ID </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>creative) </li> <li> **データフィード：**<br/>adclassificationcreative </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### サイト ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SITE_ID </li> <li> **API キー：**<br/>media.ad.siteId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>広告サイトのID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>site) </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.site） </li> </ul> | <ul> <li> **利用可能:**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>site) </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### クリエイティブ URL

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>CREATIVE_URL </li> <li> **API キー：**<br/>media.ad.creativeURL </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>広告クリエイティブのURL。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>CreativeURL） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.creativeURL） </li> </ul> | <ul> <li> **利用可能:**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>CreativeURL） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### プレースメント ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>PLACEMENT_ID </li> <li> **API キー：**<br/>media.ad.placementId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始、広告の終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>広告のプレースメントID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>placement) </li> <li> **ハートビート:**<br/> （s:meta:<br/>a.media.ad.placement） </li> </ul> | <ul> <li> **利用可能:**<br/> <i>カスタム処理ルールの使用 </i> </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> <i> </i> </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>placement) </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 広告指標 {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### 広告開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告開始 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>ビデオ広告の開始回数。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>view) </li> <li> **ハートビート:**<br/> （s:イベント:type= start）<br/> （asset:type= ad） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告開始 </li> <li> **データフィード：**<br/>videoadstart </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>view) </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### 広告完了

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>ビデオ広告の完了数。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>complete) </li> <li> **ハートビート:**<br/> （s:イベント:type= complete）<br/> （s:asset:type= ad）  </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告完了 </li> <li> **データフィード：**<br/>videoadcomplete </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>complete) </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 広告滞在時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>広告の終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 15 </li><li> **説明:**<br/>広告の視聴に費やした合計時間（秒単位、再生秒数など）。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. ad.<br/>TimePlayed） </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>広告滞在時間 </li> <li> **データフィード：**<br/>videoadtime </li> <li> **コンテキストデータ:**<br/> （a. media. ad.<br/>TimePlayed） </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### CreateAdObject API:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### CreateAdBreakObject API:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

