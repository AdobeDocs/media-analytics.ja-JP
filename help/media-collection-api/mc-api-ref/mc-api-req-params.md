---
title: リクエストパラメーター
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# リクエストパラメーター{#request-parameters}

## Analytics データ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | Adobe Analytics サーバーの URL |
| `analytics.reportSuite` | Y | `sessionStart` | Analytics レポートデータを識別する ID |
| `analytics.enableSSL` | いいえ | `sessionStart` | SSL を有効にするかどうか（true または false） |
| `analytics.visitorId` | いいえ | `sessionStart` | Adobe訪問者IDは、複数のアドビアプリケーションで使用できるカスタムIDです。 ハートビート `visitorId` はAnalyticsと等しい `VID.` |

## 訪問者データ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Experience Cloud 組織 ID。Adobe Experience Cloud エコシステム内で組織を識別します。 |
| `visitor.marketingCloudUserId` | いいえ | `sessionStart` | これは、Experience cloudユーザーID(ECID)です。 ほとんどのシナリオでは、このIDを使用してユーザーを識別します。 ハートビート `marketingCloudUserId` は、Adobe Analytics `MID` の「」と等しいです。 技術的には必須ではありませんが、このパラメーターはExperience cloudアプリのファミリーにアクセスする場合に必要です。 |
| `visitor.aamLocationHint` | いいえ | `sessionStart` | Adobe Audience Manager Edge データを提供します。 |
| `appInstallationId` | いいえ | `sessionStart` | アプリとデバイスを一意に識別する appInstallationId |

## コンテンツデータ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | コンテンツの一意の識別子 |
| `media.name` | いいえ | `sessionStart` | 人が判読可能なコンテンツの名前 |
| `media.length` | Y | `sessionStart` | コンテンツの長さ（秒） |
| `media.contentType` | Y | `sessionStart` | ストリームの形式（任意の文字列を指定できます。推奨される値は、「Live」、「VOD」または「Linear」です） |
| `media.playerName` | Y | `sessionStart` | コンテンツのレンダリングをおこなうプレーヤーの名前 |
| `media.channel` | Y | `sessionStart` | コンテンツの配布チャネル。モバイルアプリケーション名、Web サイト名またはプロパティ名を使用できます。 |
| `media.resume` | いいえ | `sessionStart` | ユーザーが（新しいセッションを開始するのではなく）前のセッションを再開しているかどうかを示します。 |
| `media.sdkVersion` | いいえ | `sessionStart` | プレーヤーで使用される SDK のバージョン |

## コンテンツ標準メタデータ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.show` | いいえ | `sessionStart` | プログラム名またはシリーズ名 |
| `media.season` | いいえ | `sessionStart` | 番組またはシリーズが属するシーズン番号 |
| `media.episode` | いいえ | `sessionStart` | エピソードの番号 |
| `media.assetId` | いいえ | `sessionStart` | TV シリーズのエピソードの識別子、ムービーアセットの識別子、ライブイベントの識別子など、ビデオアセットのコンテンツの一意の識別子。この ID は通常、EIDR、TMS／Gracenote、Rovi などのメタデータを扱う機関から取得します。その他の独自のシステムや社内システムから取得することもできます。 |
| `media.genre` | いいえ | `sessionStart` | コンテンツプロデューサーによって定義されたコンテンツのタイプ |
| `media.firstAirDate` | いいえ | `sessionStart` | コンテンツがテレビで最初に放送された日付 |
| `media.firstDigitalDate` | いいえ | `sessionStart` | コンテンツが何らかのデジタルプラットフォームで最初に放送された日付 |
| `media.rating` | いいえ | `sessionStart` | TV Parental Guidelines で定義されたレーティング |
| `media.originator` | いいえ | `sessionStart` | コンテンツの作成者 |
| `media.network` | いいえ | `sessionStart` | ネットワーク／チャネル名 |
| `media.showType` | いいえ | `sessionStart` | コンテンツのタイプ（0 ～ 3 の整数） <ul> <li>0 - エピソードそのもの </li> <li>1 - プレビュー </li> <li>2 - クリップ </li> <li>3 - その他 </li> </ul> |
| `media.adLoad` | いいえ | `sessionStart` | 読み込まれた広告のタイプ |
| `media.pass.mvpd` | いいえ | `sessionStart` | アドビの認証によって提供される MVPD |
| `media.pass.auth` | いいえ | `sessionStart` | ユーザーがアドビの認証によって認証されていることを示します（設定されている場合にのみ true になります）。 |
| `media.dayPart` | いいえ | `sessionStart` | コンテンツが放送された時刻 |
| `media.feed` | いいえ | `sessionStart` | フィードのタイプ（例：「West-HD」） |

## 広告データ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | いいえ | `adBreakStart` | 広告ブレークのわかりやすい名前 |
| `media.ad.podIndex` | Y | `adBreakStart` | ビデオ内の広告ポッドのインデックス |
| `media.ad.podSecond` | Y | `adBreakStart` | ポッドが開始された時間（秒） |
| `media.ad.podPosition` | Y | `adStart` | 広告ブレーク内の広告のインデックス（1 から開始） |
| `media.ad.name` | いいえ | `adStart` | 広告のわかりやすい名前 |
| `media.ad.id` | Y | `adStart` | 広告の名前 |
| `media.ad.length` | Y | `adStart` | ビデオ広告の長さ（秒） |
| `media.ad.playerName` | Y | `adStart` | 広告のレンダリングをおこなうプレーヤーの名前 |

## 広告標準メタデータ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | いいえ | `adStart` | 広告で取り上げられている製品の会社またはブランド |
| `media.ad.campaignId` | いいえ | `adStart` | 広告キャンペーンの ID |
| `media.ad.creativeId` | いいえ | `adStart` | 広告クリエイティブの ID |
| `media.ad.siteId` | いいえ | `adStart` | 広告サイトの ID |
| `media.ad.creativeURL` | いいえ | `adStart` | 広告クリエイティブの URL |
| `media.ad.placementId` | いいえ | `adStart` | 広告のプレースメント ID |

## チャプターデータ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | コンテンツ内のチャプターの位置を識別します。 |
| `media.chapter.offset` | Y | `chapterStart` | 再生においてチャプターが始まる時間（秒） |
| `media.chapter.length` | Y | `chapterStart` | チャプターの長さ（秒） |
| `media.chapter.friendlyName` | いいえ | `chapterStart` | チャプターのわかりやすい名前 |

## 品質データ

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | いいえ | 任意 | ストリームのビットレート |
| `media.qoe.droppedFrames` | いいえ | 任意 | ストリーム内のドロップフレームの数 |
| `media.qoe.framesPerSecond` | いいえ | 任意 | 1 秒あたりのフレーム数 |
| `media.qoe.timeToStart` | いいえ | 任意 | ユーザーが再生を押してからコンテンツが読み込まれて再生が開始されたときまでの時間（ミリ秒） |

## カリフォルニア消費者プライバシー法(CCPA)のパラメータ {#ccpa-params}

| リクエストキー | 必須 | 設定する場所 |  説明  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | いいえ | `sessionStart` | エンドユーザーがAdobe Analyticsと他のExperience cloudソリューション（Audience Managerなど）との間で共有されるデータをオプトアウトした場合にtrueに設定します |
| `analytics.optOutShare` | いいえ | `sessionStart` | エンドユーザーがフェデレーション対象のデータ（他のAdobe Analyticsクライアントなど）をオプトアウトした場合は、trueに設定します。 |

## 追加の詳細情報 {#additional-details}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. これは、既に他の Experience Cloud 製品と統合していて、MCID を既に取得している場合に便利な機能です。

>[!NOTE]
>
>Media Analytics(MA)は、Experience cloudアプリのファミリー（Adobe Analytics、Audience Manager、Targetなど）と統合されています。 これらのアプリにアクセスするには、Experience Cloud ID が必要です。_ECIDは、ほとんどのシナリオでユーザーを識別するために使用する必要があるものです。_

### appInstallationId

* **値を&#x200B;*渡さない場*合`appInstallationId`** - MAバックエンドはMCIDを生成しなくなりますが、代わりにAdobe Analyticsを使用して生成します。 MCID を送信する（MCID を取得できる場合）か、（必須の `appInstallationId` と共に）`marketingCloudOrgId` を送信してメディアコレクション API が MCID を生成してすべての呼び出しで送信できるようにすることをお勧めします。

* **値を渡す&#x200B;*場合*- MCIDは`appInstallationId`MAバックエンドで生成できます** 。この場合、と（必須）パラメータの値を渡し **`appInstallationId``marketingCloudOrgId` ます。 自分で `appInstallationId` を渡す場合は、クライアント側でその値を維持する必要があります。この値はデバイス上のアプリに対して一意である必要があり、アプリが再インストールされない限り永続的である必要があります。

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. この値は各デバイスのアプリごとに一意である必要があります。つまり、異なるデバイスで同じアプリの同じバージョンを使用する 2 人のユーザーは、それぞれ異なる（一意の）`appInstallationId` を送信する必要があります。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](/help/federated-analytics.md))

### Analyticsの従来のユーザーID(aid)および宣言済みのユーザーID(customerID)

* **analytics.aid:**

   このキーの値は、AnalyticsレガシーユーザーIDを表す文字列である必要があります
* **visitor.customerIDs:**

   このキーの値は、次の形式のオブジェクトである必要があります。

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

`visitor.customerIDs` の値には、上記の形式のオブジェクトを任意の数だけ含めることができます。

### visitor.aamLocationHint

このパラメーターは、Adobe Analyticsが顧客データをAudience Managerに送信する際に、どのAdobe Audience Manager(AAM)エッジがヒットされるかを示します。 このパラメーターを渡さない場合、アドビによって値が 1 にハードコーディングされます。これは、エンドユーザーが地理的に離れた場所（例えば、米国東部、米国西部、ヨーロッパ、アジア）でデバイスを使用する場合に特に重要です。そうでない場合、ユーザーデータは複数の AAM Edge に分散されます。

### media.resume

セッションが閉じられた後で（例えば、ユーザーが一旦ビデオから離れた後で戻ってきた結果）再開され、プレーヤーの再生ヘッドが停止された位置からビデオが再開されたことをアプリが検出した場合、**呼び出しの params バケット内でブール型のオプションの** media.resume`sessionStart` パラメーターを送信できます。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
