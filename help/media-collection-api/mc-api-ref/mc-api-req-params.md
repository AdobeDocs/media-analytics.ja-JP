---
title: ストリーミングメディアコレクション API � リクエストパラメーター
description: Media Collection API のリクエストパラメーター、リクエストキー、説明
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 100%

---

# リクエストパラメーター{#request-parameters}

## Analytics データ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | はい | string | `sessionStart` | Adobe Analytics サーバーの URL |
| `analytics.reportSuite` | はい | 文字列 | `sessionStart` | Analytics レポートデータを識別する ID |
| `analytics.enableSSL` | いいえ | ブール型 | `sessionStart` | SSL を有効にするかどうか（true または false） |
| `analytics.visitorId` | いいえ | 文字列 | `sessionStart` | Adobe 訪問者 ID は、複数のアドビアプリケーションで使用できるカスタム ID です。ハートビート `visitorId` は Analytics `VID.` と同じです。 |

## 訪問者データ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | はい | 文字列 | `sessionStart` | Experience Cloud 組織 ID。Adobe Experience Cloud エコシステム内で組織を識別します。 |
| `visitor.marketingCloudUserId` | いいえ | 文字列 | `sessionStart` | これは、Experience Cloud ユーザー ID（ECID）です。ほとんどのシナリオで、これがユーザーを識別するために使用する必要がある ID です。ハートビート `marketingCloudUserId` は、Adobe Analytics の `MID` と同じです。技術的には必須ではありませんが、このパラメーターは、Experience Cloud ファミリーのアプリにアクセスするために必要です。 |
| `visitor.aamLocationHint` | いいえ | 整数 | `sessionStart` | Adobe Audience Manager Edge データを提供します。値が入力されていない場合、値は null です。 |
| `appInstallationId` | いいえ | 文字列 | `sessionStart` | アプリとデバイスを一意に識別する appInstallationId |

## コンテンツデータ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | はい | 文字列 | `sessionStart` | コンテンツの一意の ID |
| `media.name` | いいえ | 文字列 | `sessionStart` | 人が判読可能なコンテンツの名前 |
| `media.length` | はい | 数値 | `sessionStart` | コンテンツの長さ（秒） |
| `media.contentType` | はい | 文字列 | `sessionStart` | ストリームの形式（任意の文字列を指定できます。推奨される値は、「Live」、「VOD」または「Linear」です） |
| `media.playerName` | はい | 文字列 | `sessionStart` | コンテンツのレンダリングをおこなうプレーヤーの名前 |
| `media.channel` | はい | 文字列 | `sessionStart` | コンテンツの配布チャネル。モバイルアプリケーション名、Web サイト名またはプロパティ名を使用できます。 |
| `media.resume` | いいえ | ブール型 | `sessionStart` | ユーザーが（新しいセッションを開始するに対して）以前のセッションを再開しているかどうかを示します |
| `media.sdkVersion` | いいえ | 文字列 | `sessionStart` | プレーヤーで使用される SDK のバージョン |

## コンテンツ標準メタデータ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | いいえ | 文字列 | `sessionStart` | ストリーム形式（例：「HD」） |
| `media.show` | いいえ | 文字列 | `sessionStart` | プログラム名またはシリーズ名 |
| `media.season` | いいえ | 文字列 | `sessionStart` | 番組またはシリーズが属するシーズン番号 |
| `media.episode` | いいえ | 文字列 | `sessionStart` | エピソードの番号 |
| `media.assetId` | いいえ | 文字列 | `sessionStart` | TV シリーズのエピソードの識別子、ムービーアセットの識別子、ライブイベントの識別子など、ビデオアセットのコンテンツの一意の ID。この ID は通常、EIDR、TMS／Gracenote、Rovi などのメタデータを扱う機関から取得します。その他の独自のシステムや社内システムから取得することもできます。 |
| `media.genre` | いいえ | 文字列 | `sessionStart` | コンテンツプロデューサーによって定義されたコンテンツのタイプ |
| `media.firstAirDate` | いいえ | 文字列 | `sessionStart` | コンテンツがテレビで最初に放送された日付 |
| `media.firstDigitalDate` | いいえ | 文字列 | `sessionStart` | コンテンツが何らかのデジタルプラットフォームで最初に放送された日付 |
| `media.rating` | いいえ | 文字列 | `sessionStart` | TV Parental Guidelines で定義されたレーティング |
| `media.originator` | いいえ | 文字列 | `sessionStart` | コンテンツの作成者 |
| `media.network` | いいえ | 文字列 | `sessionStart` | ネットワーク／チャネル名 |
| `media.showType` | いいえ | 文字列 | `sessionStart` | コンテンツのタイプ（0 ～ 3 の整数） <ul> <li>0 - エピソードそのもの </li> <li>1 - プレビュー </li> <li>2 - クリップ </li> <li>3 - その他 </li> </ul> |
| `media.adLoad` | いいえ | 文字列 | `sessionStart` | 読み込まれた広告のタイプ |
| `media.pass.mvpd` | いいえ | 文字列 | `sessionStart` | アドビの認証によって提供される MVPD |
| `media.pass.auth` | いいえ | 文字列 | `sessionStart` | ユーザーがアドビの認証によって認証されていることを示します（設定されている場合にのみ true になります）。 |
| `media.dayPart` | いいえ | 文字列 | `sessionStart` | コンテンツが放送された時刻 |
| `media.feed` | いいえ | 文字列 | `sessionStart` | フィードのタイプ（例：「West-HD」） |

## 広告データ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | いいえ | 文字列 | `adBreakStart` | 広告ブレークのわかりやすい名前 |
| `media.ad.podIndex` | はい | 整数 | `adBreakStart` | ビデオ内の広告ポッドのインデックス |
| `media.ad.podSecond` | はい | 数値 | `adBreakStart` | ポッドが開始された時間（秒） |
| `media.ad.podPosition` | はい | 整数 | `adStart` | 広告ブレーク内の広告のインデックス（1 から開始） |
| `media.ad.name` | いいえ | 文字列 | `adStart` | 広告のわかりやすい名前 |
| `media.ad.id` | はい | 文字列 | `adStart` | 広告の名前 |
| `media.ad.length` | はい | 数値 | `adStart` | ビデオ広告の長さ（秒） |
| `media.ad.playerName` | はい | 文字列 | `adStart` | 広告のレンダリングをおこなうプレーヤーの名前 |

## 広告標準メタデータ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | いいえ | 文字列 | `adStart` | 広告で取り上げられている製品の会社またはブランド |
| `media.ad.campaignId` | いいえ | 文字列 | `adStart` | 広告キャンペーンの ID |
| `media.ad.creativeId` | いいえ | 文字列 | `adStart` | 広告クリエイティブの ID |
| `media.ad.siteId` | いいえ | 文字列 | `adStart` | 広告サイトの ID |
| `media.ad.creativeURL` | いいえ | 文字列 | `adStart` | 広告クリエイティブの URL |
| `media.ad.placementId` | いいえ | 文字列 | `adStart` | 広告のプレースメント ID |

## チャプターデータ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | はい | 整数 | `chapterStart` | コンテンツ内のチャプターの位置を識別します。 |
| `media.chapter.offset` | はい | 数値 | `chapterStart` | 再生においてチャプターが始まる時間（秒） |
| `media.chapter.length` | はい | 数値 | `chapterStart` | チャプターの長さ（秒） |
| `media.chapter.friendlyName` | いいえ | 文字列 | `chapterStart` | チャプターのわかりやすい名前 |

## 品質データ

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | いいえ | 整数 | いずれか | ストリームのビットレート |
| `media.qoe.droppedFrames` | いいえ | 整数 | いずれか | ストリーム内のドロップフレームの数 |
| `media.qoe.framesPerSecond` | いいえ | 整数 | いずれか | 1 秒あたりのフレーム数 |
| `media.qoe.timeToStart` | いいえ | 整数 | いずれか | ユーザーが再生を押してからコンテンツが読み込まれて再生が開始されたときまでの時間（ミリ秒） |

## カリフォルニア州消費者プライバシー法（CCPA）のパラメーター {#ccpa-params}

| リクエストキー | 必須 | リクエストタイプキー | 設定する場所 |  説明  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | いいえ | ブール型 | `sessionStart` | エンドユーザーが Adobe Analytics およびその他の Experience Cloud ソリューション（例：Audience Manager）間でのデータの共有をオプトアウトした場合、true に設定します。 |
| `analytics.optOutShare` | いいえ | ブール型 | `sessionStart` | エンドユーザーが（例えば、他の Adobe Analytics クライアントに対する）データのフェデレーションをオプトアウトした場合、true に設定します。 |

## 追加の詳細情報 {#additional-details}

### visitor.marketingCloudUserId

Experience Cloud ユーザー ID（`MID` または `MCID` とも呼ばれます）は、**visitor.marketingCloudUserId** キーを使用して `params` マップに含めることで、`sessionStart` 呼び出しの際に渡します。これは、既に他の Experience Cloud 製品と統合していて、MCID を既に取得している場合に便利な機能です。

>[!NOTE]
>
>Media Analytics（MA）は、Experience Cloud ファミリーのアプリ（Adobe Analytics、Audience Manager、Target など）と統合されています。これらのアプリにアクセスするには、Experience Cloud ID が必要です。_ECID は、ほとんどのシナリオでユーザーを識別するために使用する必要があるものです。_

### appInstallationId

* **`appInstallationId` 値を渡さない場合 -** MA バックエンドは MCID を生成しなくなり、その代わりに Adobe Analytics にその操作を任せます&#x200B;*。* MCID を送信する（MCID を取得できる場合）か、（必須の `appInstallationId` と共に）`marketingCloudOrgId` を送信してメディアコレクション API が MCID を生成してすべての呼び出しで送信できるようにすることをお勧めします。

* **`appInstallationId` 値を渡す場合 -** `appInstallationId` および&#x200B;*（*&#x200B;必須の&#x200B;*）* `marketingCloudOrgId` パラメーターの値を渡すと、MA バックエンドによって MCID を生成できます。自分で `appInstallationId` を渡す場合は、クライアント側でその値を維持する必要があります。この値はデバイス上のアプリに対して一意である必要があり、アプリが再インストールされない限り永続的である必要があります。

>[!NOTE]
>
>`appInstallationId` は、アプリ&#x200B;*とデバイス*&#x200B;を一意に識別します。この値は各デバイスのアプリごとに一意である必要があります。つまり、異なるデバイスで同じアプリの同じバージョンを使用する 2 人のユーザーは、それぞれ異なる（一意の）`appInstallationId` を送信する必要があります。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

このパラメーターは、MCID が指定されていない場合に MCID の生成に必要であるだけでなく、（どの Media Analytics が[フェデレーションルールの照合](/help/federated-analytics.md)を実行するかに基づいて）Publisher ID の値としても使用されます。

### Analytics レガシーユーザー ID（aid）および宣言済みユーザー ID（customerIDs）

* **analytics.aid：**

   このキーの値は、Analytics レガシーユーザー ID を表す文字列である必要があります。
* **visitor.customerIDs：**

   このキーの値は、次の形式のオブジェクトである必要があります。

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

`visitor.customerIDs` の値には、上記の形式のオブジェクトを任意の数だけ含めることができます。

### visitor.aamLocationHint

このパラメーターは、Adobe Analytics が顧客データを Audience Manager に送信したときにどの Adobe Audience Manager（AAM）Edge がヒットするかを示します。値が入力されない場合、値は null になります。 これは、エンドユーザーが地理的に離れた場所（例えば、米国東部、米国西部、ヨーロッパ、アジア）でデバイスを使用する場合に特に重要です。そうでない場合、ユーザーデータは複数の AAM Edge に分散されます。

### media.resume

セッションが閉じられた後で（例えば、ユーザーが一旦ビデオから離れた後で戻ってきた結果）再開され、プレーヤーの再生ヘッドが停止された位置からビデオが再開されたことをアプリが検出した場合、`sessionStart` 呼び出しの params バケット内でブール型のオプションの **media.resume** パラメーターを送信できます。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
