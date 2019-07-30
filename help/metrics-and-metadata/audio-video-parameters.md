---
seo-title: オーディオおよびビデオパラメーター
title: オーディオおよびビデオパラメーター
uuid: fadfb8b- db3e-46fb- b9ad- c3a749555b2a
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# オーディオおよびビデオパラメーター{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019年2月7日に、Adobe Analytics for Videoおよびオーディオの指標名が変更されました。<i>Media Initiates</i> は <i>Media Starts</i> と呼ばれるようになります。この変更は、指標およびレポートに業界標準を反映させ、レポートで指標を簡単に識別できるようにするために行われました。

>[!NOTE]
>
>2018年9月13日以降、一部のディメンション、指標およびレポートのラベルが変更され、ビデオおよびオーディオ分析のクロスコンテンツトラッキングが可能になりました。例えば、ラベルの&#x200B;*ビデオ開始*&#x200B;が&#x200B;*メディア開始*&#x200B;に、*ビデオの長さ*&#x200B;が&#x200B;*コンテンツの長さ*&#x200B;に、*ビデオ名*&#x200B;が&#x200B;*コンテンツ名*&#x200B;に変更されています。Reports and Analytics のすべてのビデオレポートが、「ビデオ」という名前の代わりに「メディア」を使用するように更新されています。ラベルの変更によるデータ収集および履歴データへの影響はありません。Report Builder 内またはこの変更の影響を受ける可能性のある他の外部自動データプルでこれらを使用している場合は、これらの変更に注意してください。

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するオーディオおよびビデオコンテンツデータのリストを示します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なオーディオおよびビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *Send With（次を含む* ）-データの送信日時を示します。 *メディア開始* はメディア開始時に送信される解析呼び出し、 *広告開始* は広告開始時に送信される解析呼び出し、など。 *閉じる* 呼び出しは、ハートビートサーバーからメディアセッションの最後、または広告、チャプターなどの最後に直接送信されるコンパイルされた解析呼び出しです。閉じる呼び出しはネットワークパケット呼び出しでは使用できません。
   * *最小のSDK のバージョン* - パラメーターにアクセスするのに必要な SDK のバージョン。
   * *値の例* - 変数の一般的な利用方法の例。
* **ネットワークパラメーター：** Adobe Analytics またはハートビートサーバーに渡される値。この列には、Adobe Media SDK によって生成されるネットワーク呼び出しに含まれるパラメーターの名前が示されています。
* **レポート：**&#x200B;オーディオおよびビデオデータの確認方法と分析方法に関する詳細。
   * *利用可能* - デフォルトでもデータをレポートで確認できる場合は&#x200B;*可*、カスタム設定が必要な場合は&#x200B;*カスタム*。
   * *予約変数* - 予約変数で取得されるデータの形式（イベント、eVar、prop または分類）。
   * *有効期限* - データの有効期限が各ヒット後に切れるか、各訪問後に切れるかを示します。
   * *レポート名* - Adobe Aanlytics の変数のレポート名。
   * *コンテキストデータ* - レポートサーバーに渡され、処理ルールで使用される Adobe Analytics のコンテキストデータの名前。
   * *データフィード* - クリックストリームまたはライブストリームデータフィード内の変数の列の名前。
   * *Audience Manager* - Adobe Audience Manager 内の特性名。

>[!IMPORTANT]
>
>"Reporting/Reserved Variable"で説明されている変数の分類名は、「分類」として変更しないでください。\
>メディア分類は、レポートスイートがメディアトラッキングに対して有効になっているときに定義されます。アドビでは、随時、新しいプロパティを追加し、これが発生すると、レポートスイートを再度有効にして、新しいメディアプロパティにアクセスできるようにする必要があります。アドビの更新プロセス中に、変数の名前をチェックすることで、分類が有効かどうかを判定します。見つからない場合は、見つからないものが再度追加されます。

## コアのオーディオおよびビデオデータ {#section_y55_y1m_n1b}

### ストリームタイプ {#stream-type}

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.streamType </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **値の例：**<br/>"video" </li> <li> **説明:**<br/> ストリームタイプを識別します。有効な値は、"audio"、"video"、"all" です。<br/><br/>[レポートセグメント](/help/metrics-and-metadata/segments.md): <br/><br/>メディアストリームタイプ:All- <br/>すべてのメディアストリームデータをセグメント化します。ルール:コンテンツ（ID）が <br/><br/>メディアストリームタイプに存在する:オーディオ- <br/>すべてのオーディオストリームデータをセグメント化します。ルール:コンテンツ（ID）が存在し、「メディアストリームタイプ=オーディオ <br/><br/>メディアストリームタイプ」:「ビデオ」- <br/>すべてのビデオストリームデータをセグメント化します。ルール:コンテンツ（ID）が存在し、メディアストリームタイプ!= audio <br/><br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. streamType） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. streamType） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> **コンテキストデータ:**<br/> （a. media. streamType） </li> <li> **データフィード：**<br/>videostreamtype </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツ ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.id </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"4586695ABC" </li> <li>**説明:**<br/> コンテンツのコンテンツID `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. name） </li> <li> **ハートビート:**<br/> （s:asset:video_ id） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> **コンテキストデータ:**<br/> （a. media. name） </li> <li> **データフィード：**<br/>video </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツの長さ (変数)

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> VOD:128;Live:86400;線形:1800. </li><li> **説明:**<br/> Clip Length/Runtime-消費されるコンテンツの最大長（または継続時間）です。It equals the last value of `l:asset:length` from events of type Main. <br/>`l:asset:length` を設定しない場合、最後の値が使用 `l:asset:duration` されます。<br/>レポートでは、ビデオの長さは分類、コンテンツ長（変数）はeVarです。 <br/> **重要：**&#x200B;このプロパティは、進捗状況の追跡指標や分平均オーディエンスなど、複数の指標の算出に使用されます。この値が設定されていない場合、または 0 以下の場合は、これらの指標は利用できません。時間が不明なライブメディアの場合は、86400 がデフォルト値となります。<br/>Pre Version1.5.1以前 `l:asset:duration`、1.5.1の後、 `l:asset:length.`<br/> **リリース日：2018 年 9 月 14 日** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. length） </li> <li> **ハートビート:**<br/> （l:asset:length） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツの長さ (変数) </li> <li> **コンテキストデータ:**<br/> （a. media. length） </li> <li> **データフィード：**<br/>videolength </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### ビデオの長さ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> VOD:128;Live:86400;線形:1800. </li> <li> **説明:**<br/> Clip Length/Runtime-消費されるコンテンツの最大長（または継続時間）です。It equals the last value of `l:asset:length` from events of type Main. `l:asset:length` を設定しない場合、最後の値が使用 `l:asset:duration` されます。In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要：**&#x200B;このプロパティは、進捗状況の追跡指標や分平均オーディエンスなど、複数の指標の算出に使用されます。この値が設定されていない場合、または 0 以下の場合は、これらの指標は利用できません。時間が不明なライブメディアの場合は、86400 がデフォルト値となります。Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. length） </li> <li> **ハートビート:**<br/> （l:asset:length） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビデオの長さ </li> <li> **コンテキストデータ:**<br/> （a. media. length） </li> <li> **データフィード：**<br/>videoclassificationlength </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツタイプ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.contentType </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>制限付き文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"vod" </li> <li> **説明:**<br/> ストリームタイプごと **の使用可能な値**: <br/> _オーディオ：_"song"、"podcast"、"audiobook"、"radio" <br/> _ビデオ:_ "VOD"、"Live"、"Linear"、"UGC"、"DVOD" <br/> 、ユーザーはこのパラメーターのカスタム値を提供できます。This equals `s:stream:type.` If that is unset, this equals `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. contentType） </li> <li> **ハートビート:**<br/> （s:stream:type） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツタイプ </li> <li> **コンテキストデータ:**<br/> （a. contentType） </li> <li> **データフィード：**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### メディアセッション ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>バックエンドから取得 </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.8 </li> <li> **サンプル値:**<br/> 1482236761294786918253 </li> <li> **説明:**<br/> これにより、個別の再生に固有のコンテンツストリームのインスタンスが識別されます。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. vsid） </li> <li> **ハートビート:**<br/> （s:イベント:sid） </li> </ul> | <ul> <li> **利用可能：**<br/>処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **コンテキストデータ:**<br/> （a. media. vsid） </li> <li> **データフィード：**<br/>vsid </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### コンテンツプレイヤー名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.playerName </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> "Brightcove" </li> <li> **説明:**<br/> プレイヤーの名前。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.<br/>playerName) </li> <li> **ハートビート:**<br/> （s:sp:player_ name） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツプレーヤー名 </li> <li> **コンテキストデータ:**<br/> （a. media. playerName） </li> <li> **データフィード：**<br/>videoplayername </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### コンテンツチャネル

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.channel </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"Sports" </li> <li> **説明:**<br/> 配布ステーション/チャネル、またはコンテンツの再生場所。文字列であればどの値でも利用可能です。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. channel） </li> <li> **ハートビート:**<br/> （s:sp:channel） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツチャネル </li> <li> **コンテキストデータ:**<br/> （a. media. channel） </li> <li> **データフィード：**<br/>videochannel </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.channel) </li> </ul> |

### コンテンツセグメント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> "0~10" </li> <li> **説明:**<br/> 表示されたコンテンツの一部を示す間隔（分単位）。セグメントは、再生セッション中の再生ヘッドの値の最小値および最大値として計算されます。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツセグメント </li> <li> **コンテキストデータ:**<br/> （a. media. segment） </li> <li> **データフィード：**<br/>videosegment </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.segment) </li> </ul> |

### コンテンツ名 (変数)

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/>"The Big Bang Theory" </li> <li> **説明:**<br/>これは、「わかりやすい」コンテンツの「わかりやすい」（人間が読み取り可能な） `s:asset:name.`<br/>コンテンツで、「ビデオ名」は分類、ビデオ名は分類、コンテンツ名（変数）はeVarです。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.<br/>friendlyName） </li> <li> **ハートビート:**<br/> （s:asset:name） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツ名 (変数) </li> <li> **コンテキストデータ:**<br/> （a. media. friendlyName） </li> <li> **データフィード：**<br/>videoname </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### ビデオ名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/>"The Big Bang Theory" </li> <li> **説明:**<br/> これは、「わかりやすい」コンテンツの「わかりやすい」（人間が読み取り可能な） `s:asset:name.`<br/>コンテンツで、「ビデオ名」は分類、ビデオ名は分類、コンテンツ名（変数）はeVarです。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.<br/>friendlyName） </li> <li> **ハートビート:**<br/> （s:asset:name） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビデオ名 </li> <li> **コンテキストデータ:**<br/> （a. media. friendlyName） </li> <li> **データフィード：**<br/>videoclassificationname </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### ビデオパス

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"4586695ABC" </li> <li> **説明:**<br/> サイトやアプリ内のビューアのパスを追跡して、特定のビデオを表示するためにたどったパスを確認できます。整数と文字の組み合わせになります。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. name） </li> <li> **ハートビート:**<br/> （s:asset:video_ id） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>prop </li> <li> **レポート名：**<br/>ビデオパス </li> <li> **コンテキストデータ:**<br/> （a. media. name） </li> <li> **データフィード：**<br/>videopath </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.name) </li> </ul> |

### SDK バージョン

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.sdkVersion </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"2.62.0_release" </li> <li> **説明:**<br/> プレイヤーが使用するSDKバージョン。プレーヤーに対応する任意のカスタムの値が利用可能です。<br/><br/>レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.<br/>sdkVersion) </li> <li> **ハートビート:**<br/> （s:sp:sdk） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. sdkVersion） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL バージョン

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **説明:**<br/> トラッキングセッションに使用されるハートビートSDKバージョン。<br/><br/>レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。<br/><br/>[MediaHeartbeat. version（）;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.<br/>vhlVersion） </li> <li> **ハートビート:**<br/> （s:sp:hb_ version） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **コンテキストデータ:**<br/> （a. media. vhlVersion） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 標準オーディオおよびビデオメタデータ{#section_pfc_hbm_n1b}

### 番組

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SHOW </li> <li> **API キー：**<br/>media.show </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "Modern Family""Blacklist""New girl" </li> <li> **説明:**<br/> プログラム/シリーズ名 <br/>プログラム名は、番組がシリーズの一部である場合にのみ必要です。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. show） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. show） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>番組 </li> <li> **コンテキストデータ:**<br/> （a. media. show） </li> <li> **データフィード：**<br/>videoshow </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.show) </li> </ul> |

### ストリーム形式

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>STREAM_FORMAT </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"Live" </li> <li> **説明:**<br/> ストリームの形式（ライブ、VOD、リニア）。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. format） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. format） </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **コンテキストデータ:**<br/> （a. media. format） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.format) </li> </ul> |

### シーズン

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SEASON </li> <li> **API キー：**<br/>media.season </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "2" </li> <li> **説明:**<br/> 番組が属する季節番号。シーズンシリーズは、番組がシリーズの一部である場合にのみ必要です。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media.季節） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media.季節） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>シーズン </li> <li> **コンテキストデータ:**<br/> （a. media.季節） </li> <li> **データフィード：**<br/>videoseason </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.season) </li> </ul> |

### エピソード

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>EPISODE </li> <li> **API キー：**<br/>media.episode </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "13" </li> <li> **説明:**<br/> エピソードの数。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. episode） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. episode） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エピソード </li> <li> **コンテキストデータ:**<br/> （a. media. episode） </li> <li> **データフィード：**<br/>videoepisode </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.episode) </li> </ul> |

### アセット ID

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ASSET_ID </li> <li> **API キー：**<br/>media.assetId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "89745363" </li> <li> **説明:**<br/> これは、テレビシリーズのエピソード識別子、ムービーアセット識別子、ライブイベント識別子など、メディアアセットのコンテンツの一意の識別子です。この ID は通常、EIDR、TMS／Gracenote、Rovi などのメタデータを扱う機関から取得します。その他の独自のシステムや社内システムから取得することもできます。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. asset） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. asset） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>アセット ID </li> <li> **コンテキストデータ:**<br/> （a. media. asset） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.asset) </li> </ul> |

### ジャンル

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>GENRE </li> <li> **API キー：**<br/>media.genre </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> 「ドラマ」、「コメディ」 </li> <li> **説明:**<br/> コンテンツプロデューサーによって定義されるコンテンツのタイプまたはグループ化。変数の実装では、値をコンマで区切る必要があります。レポートでは、リスト eVar は各値を行項目に分割し、各行項目は同じ指標の重みを受け取ります。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. genre） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. genre） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>リスト eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ジャンル </li> <li> **コンテキストデータ:**<br/> （a. media. genre） </li> <li> **データフィード：**<br/>videogenre </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.genre) </li> </ul> |

### 初回放送日

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FIRST_AIR_DATE </li> <li> **API キー：**<br/>media.firstAirDate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "2016-01-25" </li> <li> **説明:**<br/> テレビで最初に放送されたコンテンツの日付。どのような形式でも問題ありませんが、YYYY-MM-DD の形式にすることをお勧めします。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. airDate） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. airDate） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>初回放送日 </li> <li> **コンテキストデータ:**<br/> （a. media. airDate） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### 初回デジタル日

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FIRST_DIGITAL_DATE </li> <li> **API キー：**<br/>media.firstDigitalDate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "2016-01-25" </li> <li> **説明:**<br/> デジタルチャネルまたはプラットフォームで最初に放送されたコンテンツの日付。どのような形式でも問題ありませんが、YYYY-MM-DD の形式にすることをお勧めします。 </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. digitalDate） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. digitalDate） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>初回デジタル日 </li> <li> **コンテキストデータ:**<br/> （a. media. digitalDate） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### コンテンツ評価

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>RATING </li> <li> **API キー：**<br/>media.rating </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> TVV、TVG、TVPG、TVMA </li> <li> **説明:**<br/> テレビの親ガイドラインで定義されているレーティング。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. rating） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. rating） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>コンテンツ評価 </li> <li> **コンテキストデータ:**<br/> （a. media. rating） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.rating) </li> </ul> |

### 作成者

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ORIGINATOR </li> <li> **API キー：**<br/>media.originator </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "Warner兄弟」、「ソニー」、「ディズニー」 </li> <li> **説明:**<br/> コンテンツの作成者。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. originator） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. originator） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>作成者 </li> <li> **コンテキストデータ:**<br/> （a. media. originator） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.originator) </li> </ul> |

### ネットワーク

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>NETWORK </li> <li> **API キー：**<br/>media.network </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "Fox"、"Bravo"、"ESPN" </li> <li> **説明:**<br/> ネットワーク/チャネル名。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. network） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. network） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ネットワーク </li> <li> **コンテキストデータ:**<br/> （a. media. network） </li> <li> **データフィード：**<br/>videonetwork </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.network) </li> </ul> |

### 番組タイプ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SHOW_TYPE </li> <li> **API キー：**<br/>media.showType </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "0"=フルエピソード;"1"= Preview/trailer;"2"= Clip;"3"= Other. </li> <li> **説明:**<br/> コンテンツのタイプ。0~3の整数で表されます。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. type） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. type） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>番組タイプ </li> <li> **コンテキストデータ:**<br/> （a. media. type） </li> <li> **データフィード：**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>MVPD </li> <li> **API キー：**<br/>media.pass.mvpd </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "Comcast"、"DirectTV"、"Social" </li> <li> **説明:**<br/> Adobe認証によって提供されるVPD。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. pass. mvpd） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>MVPD </li> <li> **コンテキストデータ:**<br/> （a. media. pass. mvpd） </li> <li> **データフィード：**<br/>videomvpd </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 認証済み

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>AUTHORIZED </li> <li> **API キー：**<br/>media.pass.auth </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "TRUE" </li> <li> **説明:**<br/> ユーザーはAdobe認証を通じて認証されています。<br/>**重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. pass. auth） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. pass.<br/>auth） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>認証済み </li> <li> **コンテキストデータ:**<br/> （a. media. pass. auth） </li> <li> **データフィード：**<br/>videoauthorized </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 日パート

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>DAY_PART </li> <li> **API キー：**<br/>media.dayPart </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/> </li> <li> **説明:**<br/> コンテンツがブロードキャストまたは再生された時刻を定義するプロパティ。お客様の必要に応じて、任意の値を設定できます。  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. dayPart） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. dayPart） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>日パート </li> <li> **コンテキストデータ:**<br/> （a. media. dayPart） </li> <li> **データフィード：**<br/>videodaypart </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### メディアフィードのタイプ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FEED </li> <li> **API キー：**<br/>media.feed </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **サンプル値:**<br/> "East- HD"、"West- HD"、"East- SD" </li> <li> **説明:**<br/> フィードのタイプ。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. feed） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. feed） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>メディアフィードのタイプ </li> <li> **コンテキストデータ:**<br/> （a. media. feed） </li> <li> **データフィード：**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.feed) </li> </ul> |

### 作者名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.artist </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"The Beatles" </li> <li> **説明:**<br/> アーティストの名前。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. artist） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. artist） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. artist） </li> <li> **データフィード：**<br/>videoaudioartist </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.artist) </li> </ul> |

### アルバム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.album </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"Revolver" </li> <li> **説明:**<br/> アルバムの名前。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. album） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. album） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. album） </li> <li> **データフィード：**<br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.album) </li> </ul> |

### ラベル

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.label </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"Revolver" </li> <li> **説明:**<br/> レコードラベルの名前。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. label） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. label） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. label） </li> <li> **データフィード：**<br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.label) </li> </ul> |

### 作成者

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.author </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"John Kennedy Toole" </li> <li> **説明:**<br/> 発言者の名前。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. author） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. author） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. author） </li> <li> **データフィード：**<br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.author) </li> </ul> |

### ステーション

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.station </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"NPR" </li> <li> **説明:**<br/> ラジオ局の名前/ID。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. station） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. station） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. station） </li> <li> **データフィード：**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.station) </li> </ul> |

### 発行者

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.publisher </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア開始、メディア終了 </li> <li> **最小のSDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **値の例：**<br/>"Random Bauhaus" </li> <li> **説明:**<br/> オーディオコンテンツ投稿者の名前。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. publisher） </li> <li> **ハートビート:**<br/> （s:meta:<br/>a. media. publisher） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> **コンテキストデータ:**<br/> （a. media. publisher） </li> <li> **データフィード：**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## オーディオおよびビデオ指標 {#section_3D5F9C555274428AA6030D07596177E9}

### メディア開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定</li> <li> **API キー：**<br/>なし</li> <li> **型：**<br/>文字列</li> <li> **送信先:**<br/> メディア開始</li> <li> **最小のSDK のバージョン：**&#x200B;すべて可</li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> メディアの読み込みイベント。（ユーザーが&#x200B;_再生_&#x200B;ボタンをクリックしたときに発生します）。プリロール広告やバッファリング、エラーなどがあった場合でもカウントされます。<br/>**重要：**&#x200B;設定されている場合は true のみを返します。If it is not set, no value is returned.  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. view） </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= start） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名:**<br/> メディア開始 </li> <li> **コンテキストデータ:**<br/> （a. media. view） </li> <li> **データフィード：**<br/>videostart </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.view) </li> </ul> |

### コンテンツ開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> メディアの最初のフレームが消費されます。If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ開始 </li> <li> **コンテキストデータ:**<br/> （a. media. play） </li> <li> **データフィード：**<br/>videoplay </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.play) </li> </ul> |

### コンテンツ完了 {#content-complete}

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 最後まで視聴されたストリーム。これは、ユーザーがストリーム全体を視聴またはリッスンするという意味ではありません。これらは事前にスキップされている可能性があります。これは、ユーザーがストリームの最後に到達し、100%に到達したことを意味します。<br/>[「セッション終了」も参照してください](quality-parameters.md#session-end)<br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= complete） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ完了 </li> <li> **コンテキストデータ:**<br/> （a. media. complete） </li> <li> **データフィード：**<br/>videocomplete </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.complete) </li> </ul> |

### コンテンツ視聴時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 105 </li> <li> **説明:**<br/> メインコンテンツのPLAYタイプのすべてのイベントのイベント時間（秒単位）を合計します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ視聴時間 </li> <li> **コンテキストデータ:**<br/> （a. media. timePlayed） </li> <li> **データフィード：**<br/>videotime </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### メディア視聴時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 120 </li> <li> **説明:**<br/> メインコンテンツと広告コンテンツの両方のタイプのPLAYのイベント時間（秒単位）を合計します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>メディア視聴時間 </li> <li> **コンテキストデータ:**<br/> （a. media. totalTimePlayed） </li> <li> **データフィード：**<br/>videototaltime </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### ユニーク再生時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 94 </li> <li> **説明:**<br/> セッション中に再生されるコンテンツの固有セグメントの数（秒単位）。視聴者がコンテンツの同じセグメントを複数回視聴しているシークバックシナリオでの再生時間を除外します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>カスタム </li> <li> **コンテキストデータ:**<br/> （a. media. uniqueTimePlayed） </li> <li> **データフィード：**<br/>videouniquetimeplayed </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. uniqueTimePlayed） </li> </ul> |

### 10%プログレスマーカー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再生ヘッドは、長さに基づいてコンテンツの10%マーカーを渡します。巻き戻しのシークがあった場合でも、このマーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>10％プログレスマーカー </li> <li> **コンテキストデータ:**<br/> （a. media. progress10） </li> <li> **データフィード：**<br/>videoprogress10 </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### 25%プログレスマーカー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再生ヘッドはコンテンツの長さに基づいて25%のコンテンツのマーカーを渡します。巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>25％プログレスマーカー </li> <li> **コンテキストデータ:**<br/> （a. media. progress25） </li> <li> **データフィード：**<br/>videoprogress25 </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### 5%プログレスマーカー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再生ヘッドはコンテンツの長さに基づいてコンテンツの50%マーカーを渡します。巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>50％プログレスマーカー </li> <li> **コンテキストデータ:**<br/> （a. media. progress50） </li> <li> **データフィード：**<br/>videoprogress50 </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### 75%プログレスマーカー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> **該当なし** </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再生ヘッドはコンテンツの長さに基づいて75%のコンテンツのマーカーを渡します。巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>75％プログレスマーカー </li> <li> **コンテキストデータ:**<br/> （a. media. progress75） </li> <li> **データフィード：**<br/>videoprogress75 </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### 95%プログレスマーカー

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再生ヘッドはコンテンツの長さに基づいてコンテンツの95%マーカーを渡します。巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>95％プログレスマーカー </li> <li> **コンテキストデータ:**<br/> （a. media. progress95） </li> <li> **データフィード：**<br/>videoprogress95 </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### 分平均オーディエンス

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>1 以上 </li> <li> **説明:**<br/> 分平均オーディエンス指標は、1つの特定のメディア項目の合計コンテンツ滞在時間として、すべての再生セッションでの長さで割って算出されます。 <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>分平均オーディエンス </li> <li> **コンテキストデータ:**<br/> （a. media. averageMinuteAudience） </li> <li> **データフィード：**<br/>videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 推定ストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **サンプル値:**<br/> 1-19分間再生する場合、 <br/>2-31分間再生する場合、 <br/>3-78分間再生する場合。 </li> <li> **説明:**<br/> 個々のコンテンツごとのビデオストリームまたはオーディオストリームの予測数。コンテンツと広告を含む再生時間 30 分ごとに増加します。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。<br/><br/>ストリームは、次のように、（totalTimePlayed= Video Total Time）に `ms_s` 基づいて30分ごとにカウントされます。 <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **コンテキストデータ:**<br/> （a. media. estimatedStreams） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. estimatedStreams） </li> </ul> |

### 一時停止の影響を受けたストリーム

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> この値はtrueまたはfalseです。It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= pause） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止の影響を受けたストリーム </li> <li> **コンテキストデータ:**<br/> （a. media. pause） </li> <li> **データフィード：**<br/>videopause </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.pause) </li> </ul> |

### 一時停止イベント

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **サンプル値:**<br/> 2 </li> <li> **説明:**<br/> この指標は、再生セッション中に発生した一時停止期間のカウントとして計算されます。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= pause） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止イベント </li> <li> **コンテキストデータ:**<br/> （a. media. pauseCount） </li> <li> **データフィード：**<br/>videopausecount </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 一時停止時間合計

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **サンプル値:**<br/> 190 </li> <li> **説明:**<br/> PAUSEタイプのすべてのイベントの時間（秒単位）を合計します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止時間合計 </li> <li> **コンテキストデータ:**<br/> （a. media. pauseTime） </li> <li> **データフィード：**<br/>videopausetime </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### コンテンツ再開

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> **media.resume** </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> 再開は、30分以上のバッファー、一時停止または停止期間後に再開される各再生に対してカウントされます。また、この値がVideoInfo trackPlayで設定されている場合は、その再生ごとにカウントされます。 <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= resume） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ再開 </li> <li> **コンテキストデータ:**<br/> （a. media. resume） </li> <li> **データフィード：**<br/>videoresume </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.resume) </li> </ul> |

### コンテンツセグメント視聴回数

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **説明:**<br/> メインコンテンツのビュー数。A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツセグメント視聴回数 </li> <li> **コンテキストデータ:**<br/> （a. media. segmentView） </li> <li> **データフィード：**<br/>videosegmentviews </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

