---
title: Streaming Media Services APIのリクエストパラメーター
description: Media Collection APIのリクエストパラメーター、リクエストキー、説明とは何ですか。
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/6SPeRxCbhd8xZE-u0PlNpqXpZ9JWAS5hi41f7mjTBe0
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 1337
ht-degree: 86%

---

# リクエストパラメーター{#request-parameters}

## Analytics データ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | はい | string | `sessionStart` | Adobe Analytics サーバーの URL |
| `analytics.reportSuite` | はい | string | `sessionStart` | Analytics レポートデータを識別する ID |
| `analytics.enableSSL` | いいえ | ブール型 | `sessionStart` | SSL を有効にするかどうか（true または false） |
| `analytics.visitorId` | いいえ | string | `sessionStart` | Adobe 訪問者 ID は、複数のアドビアプリケーションで使用できるカスタム ID です。 ハートビート `visitorId` は Analytics `VID.` と同じです。 |

## 訪問者データ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | はい | string | `sessionStart` | IMS組織ID。Adobe CX Enterprise内の組織を識別します。 |
| `visitor.marketingCloudUserId` | いいえ | string | `sessionStart` | Experience Cloud ユーザーID （ECID）。 ほとんどのシナリオで、これがユーザーを識別するために使用する必要がある ID です。 ハートビート `marketingCloudUserId` は、Adobe Analytics の `MID` と同じです。 このパラメーターは技術的には必要ありませんが、CX Enterpriseのアプリやサービスにアクセスする場合は必要です。 |
| `visitor.aamLocationHint` | いいえ | 整数 | `sessionStart` | Adobe Audience Manager Edge データを提供します。 値が入力されない場合、値は null になります。 |
| `appInstallationId` | いいえ | string | `sessionStart` | アプリとデバイスを一意に識別する appInstallationId |

## コンテンツデータ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.id` | はい | string | `sessionStart` | コンテンツの一意の ID |
| `media.name` | いいえ | string | `sessionStart` | 人が判読可能なコンテンツの名前 |
| `media.length` | はい | number | `sessionStart` | コンテンツの長さ（秒） |
| `media.contentType` | はい | string | `sessionStart` | ストリームの形式（任意の文字列を指定できます。推奨される値は、「Live」、「VOD」または「Linear」です） |
| `media.playerName` | はい | string | `sessionStart` | コンテンツのレンダリングをおこなうプレーヤーの名前 |
| `media.channel` | はい | string | `sessionStart` | コンテンツの配布チャネル。 モバイルアプリケーション名、Web サイト名またはプロパティ名を使用できます。 |
| `media.resume` | いいえ | ブール型 | `sessionStart` | ユーザーが（新しいセッションを開始するに対して）以前のセッションを再開しているかどうかを示します |
| `media.sdkVersion` | いいえ | string | `sessionStart` | プレーヤーで使用される SDK のバージョン |

## コンテンツ標準メタデータ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | いいえ | string | `sessionStart` | ストリーミング形式（例：「HD」） |
| `media.show` | いいえ | string | `sessionStart` | プログラム名またはシリーズ名 |
| `media.season` | いいえ | string | `sessionStart` | 番組またはシリーズが属するシーズン番号 |
| `media.episode` | いいえ | string | `sessionStart` | エピソードの番号 |
| `media.assetId` | いいえ | string | `sessionStart` | TV シリーズのエピソードの識別子、ムービーアセットの識別子、ライブイベントの識別子など、ビデオアセットのコンテンツの一意の ID。 この ID は通常、EIDR、TMS／Gracenote、Rovi などのメタデータを扱う機関から取得します。 その他の独自のシステムや社内システムから取得することもできます。 |
| `media.genre` | いいえ | string | `sessionStart` | コンテンツプロデューサーによって定義されたコンテンツのタイプ |
| `media.firstAirDate` | いいえ | string | `sessionStart` | コンテンツがテレビで最初に放送された日付 |
| `media.firstDigitalDate` | いいえ | string | `sessionStart` | コンテンツが何らかのデジタルプラットフォームで最初に放送された日付 |
| `media.rating` | いいえ | string | `sessionStart` | TV Parental Guidelines で定義されたレーティング |
| `media.originator` | いいえ | string | `sessionStart` | コンテンツの作成者 |
| `media.network` | いいえ | string | `sessionStart` | ネットワーク／チャネル名 |
| `media.showType` | いいえ | string | `sessionStart` | コンテンツのタイプ（0 ～ 3 の整数） <ul> <li>0 - エピソードそのもの </li> <li>1 - プレビュー </li> <li>2 - クリップ </li> <li>3 - その他 </li> </ul> |
| `media.adLoad` | いいえ | string | `sessionStart` | 読み込まれた広告のタイプ |
| `media.pass.mvpd` | いいえ | string | `sessionStart` | アドビの認証によって提供される MVPD |
| `media.pass.auth` | いいえ | string | `sessionStart` | ユーザーがアドビの認証によって認証されていることを示します（設定されている場合にのみ true になります）。 |
| `media.dayPart` | いいえ | string | `sessionStart` | コンテンツが放送された時刻 |
| `media.feed` | いいえ | string | `sessionStart` | フィードのタイプ（例：「West-HD」） |

## 広告データ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | いいえ | string | `adBreakStart` | 広告ブレークのわかりやすい名前 |
| `media.ad.podIndex` | はい | 整数 | `adBreakStart` | ビデオ内の広告ポッドのインデックス |
| `media.ad.podSecond` | はい | number | `adBreakStart` | ポッドが開始された時間（秒） |
| `media.ad.podPosition` | はい | 整数 | `adStart` | 広告ブレーク内の広告のインデックス（1 から開始） |
| `media.ad.name` | いいえ | string | `adStart` | 広告のわかりやすい名前 |
| `media.ad.id` | はい | string | `adStart` | 広告の名前 |
| `media.ad.length` | はい | number | `adStart` | ビデオ広告の長さ（秒） |
| `media.ad.playerName` | はい | string | `adStart` | 広告のレンダリングをおこなうプレーヤーの名前 |

## 広告標準メタデータ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | いいえ | string | `adStart` | 広告で取り上げられている製品の会社またはブランド |
| `media.ad.campaignId` | いいえ | string | `adStart` | 広告キャンペーンの ID |
| `media.ad.creativeId` | いいえ | string | `adStart` | 広告クリエイティブの ID |
| `media.ad.siteId` | いいえ | string | `adStart` | 広告サイトの ID |
| `media.ad.creativeURL` | いいえ | string | `adStart` | 広告クリエイティブの URL |
| `media.ad.placementId` | いいえ | string | `adStart` | 広告のプレースメント ID |

## チャプターデータ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | はい | 整数 | `chapterStart` | コンテンツ内のチャプターの位置を識別します。 |
| `media.chapter.offset` | はい | number | `chapterStart` | 再生においてチャプターが始まる時間（秒） |
| `media.chapter.length` | はい | number | `chapterStart` | チャプターの長さ（秒） |
| `media.chapter.friendlyName` | いいえ | string | `chapterStart` | チャプターのわかりやすい名前 |

## 品質データ

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | いいえ | 整数 | いずれか | 平均ビットレート（bps）。 平均ビットレートは、再生セッション中に発生した再生時間に関連するすべてのビットレート値の加重平均として計算されます。 |
| `media.qoe.droppedFrames` | いいえ | 整数 | いずれか | ストリーム内のドロップフレームの数 |
| `media.qoe.framesPerSecond` | いいえ | 整数 | いずれか | 1 秒あたりのフレーム数 |
| `media.qoe.timeToStart` | いいえ | 整数 | いずれか | ユーザーが再生を押してからコンテンツが読み込まれて再生が開始されたときまでの時間（ミリ秒） |

## カリフォルニア州消費者プライバシー法（CCPA）のパラメーター {#ccpa-params}

| リクエストキー | 必須 | リクエストタイプキー | 次に設定… | 説明 |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | いいえ | ブール型 | `sessionStart` | エンドユーザーが、Adobe Analyticsと他のCX Enterprise ソリューション（Audience Managerなど）間で共有されるデータをオプトアウトした場合にtrueに設定します。 |
| `analytics.optOutShare` | いいえ | ブール型 | `sessionStart` | エンドユーザーが（例えば、他の Adobe Analytics クライアントに対する）データのフェデレーションをオプトアウトした場合、true に設定します。 |

## 追加の詳細情報 {#additional-details}

### visitor.marketingCloudUserId

Experience Cloud ユーザー ID（`MID` または `MCID` とも呼ばれます）は、**visitor.marketingCloudUserId** キーを使用して `params` マップに含めることで、`sessionStart` 呼び出しの際に渡します。 これは、既に他のCX Enterprise製品と統合しており、MCIDを取得済みの場合に便利な機能です。

>[!NOTE]
>
>Media Analytics （MA）は、CX Enterprise ファミリーのアプリケーション（Adobe Analytics、Audience Manager、Targetなど）と統合されています。 これらのアプリにアクセスするには、Experience Cloud ID が必要です。 _ECID は、ほとんどのシナリオでユーザーを識別するために使用する必要があるものです。_

### appInstallationId

* **`appInstallationId` 値を渡さない場合 -** MA バックエンドは MCID を生成しなくなり、その代わりに Adobe Analytics にその操作を任せます&#x200B;*。* アドビのレコメンデーションは、MCID を送信する（MCID を取得できる場合）か、（必須の `appInstallationId` と共に）`marketingCloudOrgId` を送信してメディアコレクション API が MCID を生成してすべての呼び出しで送信できるようにすることです。

* **`appInstallationId` 値を渡す場合 -** `appInstallationId` および&#x200B;*（*&#x200B;必須の&#x200B;*）* `marketingCloudOrgId` パラメーターの値を渡すと、MA バックエンドによって MCID を生成できます。 自分で `appInstallationId` を渡す場合は、クライアント側でその値を維持する必要があります。 この値はデバイス上のアプリに対して一意である必要があり、アプリが再インストールされない限り永続的である必要があります。

>[!NOTE]
>
>`appInstallationId` は、アプリ&#x200B;*とデバイス*&#x200B;を一意に識別します。 この値は各デバイスのアプリごとに一意である必要があります。つまり、異なるデバイスで同じアプリの同じバージョンを使用する 2 人のユーザーは、それぞれ異なる（一意の）`appInstallationId` を送信する必要があります。

<!-- 
Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> 
-->

### visitor.marketingCloudOrgId

このパラメーターは、MCID が指定されていない場合に MCID の生成に必要であるだけでなく、（どの Media Analytics が[フェデレーションルールの照合](/help/use-cases/federated-media.md)を実行するかに基づいて）Publisher ID の値としても使用されます。

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

このパラメーターは、Adobe Analytics が顧客データを Audience Manager に送信したときにどの Adobe Audience Manager（AAM）Edge がヒットするかを示します。 値が入力されない場合、値は null になります。 これは、エンドユーザーが地理的に離れた場所（例えば、米国東部、米国西部、ヨーロッパ、アジア）でデバイスを使用する場合に特に重要です。 そうでない場合、ユーザーデータは複数の AAM Edge に分散されます。

### media.resume

セッションが閉じられた後で（例えば、ユーザーが一旦ビデオから離れた後で戻ってきた結果）再開され、プレーヤーの再生ヘッドが停止された位置からビデオが再開されたことをアプリが検出した場合、`sessionStart` 呼び出しの params バケット内でブール型のオプションの **media.resume** パラメーターを送信できます。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
