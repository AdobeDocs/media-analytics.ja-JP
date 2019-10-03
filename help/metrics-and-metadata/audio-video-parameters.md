---
seo-title: オーディオおよびビデオパラメーター
title: オーディオおよびビデオパラメーター
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: a3e400a135af532be4320c7510032d518c4b6865

---


# オーディオおよびビデオパラメーター{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019年2月7日に、Adobe Analytics for Video and Audioが指標名の変更をリリースしました。 <i>Media Initiates</i> は <i>Media Starts</i> と呼ばれるようになります。この変更は、指標とレポートに業界標準を反映し、レポートで指標を簡単に識別できるようにするために行われました。

>[!NOTE]
>
>2018年9月13日より、一部のディメンション、指標およびレポートのラベルに変更が加えられ、ビデオおよびオーディオ分析のクロスコンテンツ追跡が可能になりました。 例えば、ラベルの&#x200B;*ビデオ開始*&#x200B;が&#x200B;*メディア開始*&#x200B;に、*ビデオの長さ*&#x200B;が&#x200B;*コンテンツの長さ*&#x200B;に、*ビデオ名*&#x200B;が&#x200B;*コンテンツ名*&#x200B;に変更されています。Reports and Analytics のすべてのビデオレポートが、「ビデオ」という名前の代わりに「メディア」を使用するように更新されています。ラベルの変更によるデータ収集および履歴データへの影響はありません。Report Builder 内またはこの変更の影響を受ける可能性のある他の外部自動データプルでこれらを使用している場合は、これらの変更に注意してください。

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するオーディオおよびビデオコンテンツデータのリストを示します。

表のデータの説明は次のとおりです。

* **実装：**&#x200B;実装に関する値と要件の詳細。
   * *キー* - 変数。アプリで手動で設定するか、Adobe Media SDK によって自動的に設定されます。
   * *必須* - 基本的なオーディオおよびビデオトラッキングでパラメーターが必須かどうかを表します。
   * *型* - 設定する変数の型（文字列または数値）を表します。
   * *Sent With* - Indicates when the data is sent: *Media Start* is the analytics call sent on media start, *Ad Start* is the analytics call sent on ad start, and so on; the *Close* calls are the compiled analytics calls sent directly from the heartbeat server to the analytics server at the end of the media session, or the end of the ad, chapter, etc. The close calls are not available in network packet calls.
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
>Do not change the classification names for any variables listed below that are described under Reporting/Reserved Variable as "classification".\
>The media classifications are defined when a report suite is enabled for media tracking. From time to time, Adobe adds new properties, and, when this occurs, customers must re-enable their report suites to get access to the new media properties. During the update process Adobe determines whether the classifications are enabled by checking the names of the variables. いずれかが見つからない場合は、見つからないものが再度追加されます。

## コアのオーディオおよびビデオデータ {#section_y55_y1m_n1b}

### ストリームタイプ {#stream-type}

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.streamType </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **値の例：**<br/>"video" </li> <li> ****<br/> 説明：ストリームタイプを識別します。 有効な値は、"audio"、"video"、"all" です。<br/><br/>[レポートセグメント](/help/metrics-and-metadata/segments.md):メデ <br/><br/>ィアストリームタイプ：すべて — すべてのメ <br/>ディアストリームデータをセグメント化します。ルール：コンテンツ(ID)が存在するメディア <br/><br/>ストリームタイプ：オーディオ — すべ <br/>てのオーディオストリームデータをセグメント化ルール：コンテンツ(ID)が存在し、メディアストリームタイプ=オーディオメ <br/><br/>ディアストリームタイプ："ビデオ" — すべてのビ <br/>デオストリームデータのセグメント化；ルール：コンテンツ(ID)が存在し、メディアストリームタイプ！= audio <br/><br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.streamType) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> ****<br/> Context Data: (a.media.streamType) </li> <li> **データフィード：**<br/>videostreamtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツ ID

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.id </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"4586695ABC" </li> <li>****<br/> 説明：コンテンツのコンテンツID。他の業界/CMS IDと結び付けるのに使用でき、 `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> ハートビート：(s:asset:video_id) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> ****<br/> コンテキストデータ：(a.media.name) </li> <li> **データフィード：**<br/>video </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツの長さ (変数)

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：VOD:128;ライブ：86400;線形：1800。 </li><li> ****<br/> 説明：クリップの長さ/実行時間 — 使用されるコンテンツの最大の長さ（または時間）（秒）。 It equals the last value of `l:asset:length` from events of type Main. <br/>が設 `l:asset:length` 定されていない場合は、の最後の値が使用 `l:asset:duration` されます。 <br/>レポートでは、ビデオの長さが分類、コンテンツの長さ（変数）がeVARです。  <br/> **重要：**&#x200B;このプロパティは、進捗状況の追跡指標や分平均オーディエンスなど、複数の指標の算出に使用されます。この値が設定されていない場合、または 0 以下の場合は、これらの指標は利用できません。時間が不明なライブメディアの場合は、86400 がデフォルト値となります。<br/>バージョン1.5.1より前のバージョンは、次のとおりで `l:asset:duration`す。1.5.1の後で、これは、 `l:asset:length.`<br/> **リリース日：2018 年 9 月 14 日** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> ハートビート：(l:asset:length) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツの長さ (変数) </li> <li> ****<br/> コンテキストデータ：(a.media.length) </li> <li> **データフィード：**<br/>videolength </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### ビデオの長さ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.length </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：VOD:128;ライブ：86400;線形：1800。 </li> <li> ****<br/> 説明：クリップの長さ/実行時間 — 使用されるコンテンツの最大の長さ（または時間）（秒）。 It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要：**&#x200B;このプロパティは、進捗状況の追跡指標や分平均オーディエンスなど、複数の指標の算出に使用されます。この値が設定されていない場合、または 0 以下の場合は、これらの指標は利用できません。時間が不明なライブメディアの場合は、86400 がデフォルト値となります。Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> ハートビート：(l:asset:length) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビデオの長さ </li> <li> ****<br/> Context Data: (a.media.length) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### コンテンツタイプ

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.contentType </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>制限付き文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"vod" </li> <li> **Description:**<br/> Available values per **Stream Type**: <br/> _オーディオ：_"song"、"podcast"、"audiobook"、"radio" <br/> __ ビデオ：「VoD」、「Live」、「Linear」、「UGC」、「DVoD」このパラメーターのカスタム値を <br/> 指定することができます。 「次の値に等し `s:stream:type.` い」が設定されていない場合、「次の値」が `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.contentType) </li> <li> ****<br/> ハートビート：(s:stream:type) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツタイプ </li> <li> ****<br/> コンテキストデータ：(a.contentType) </li> <li> **データフィード：**<br/>videocontenttype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### メディアセッション ID

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>バックエンドから取得 </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.8 </li> <li> ****<br/> サンプル値：1482236761294786918253 </li> <li> ****<br/> 説明：これは、個々の再生に固有のコンテンツストリームのインスタンスを識別します。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.vsid) </li> <li> ****<br/> ハートビート：(s:event:sid) </li> </ul> | <ul> <li> **利用可能：**<br/>処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> ****<br/> コンテキストデータ：(a.media.vsid) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vsid) </li> </ul> |

### メディアダウンロードフラグ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>バックエンドから取得 </li> <li> **必須：**<br/>いいえ </li> <li> ****<br/> タイプ：boolean </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 2.2 </li> <li> ****<br/> サンプル値：true </li> <li> ****<br/> 説明：ダウンロードされたコンテンツメディアセッションの再生によってヒットが生成される場合は、trueに設定します。 ダウンロードされたコンテンツが再生されない場合は存在しません。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.downloaded) </li> <li> ****<br/> ハートビート：(s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **Context Data:**<br/> (a.media.downloaded) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### コンテンツプレイヤー名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.playerName </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> Sample value: "Brightcove" </li> <li> ****<br/> Description: Name of the player.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> ****<br/> ハートビート：(s:sp:player_name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツプレーヤー名 </li> <li> ****<br/> Context Data: (a.media.playerName) </li> <li> **データフィード：**<br/>videoplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.playerName) </li> </ul> |

### コンテンツチャネル

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.channel </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"Sports" </li> <li> ****<br/> 説明：配布ステーション/チャネル、またはコンテンツが再生される場所。 文字列であればどの値でも利用可能です。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeats: (s:sp:channel) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツチャネル </li> <li> ****<br/> Context Data: (a.media.channel) </li> <li> **データフィード：**<br/>videochannel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.channel) </li> </ul> |

### コンテンツセグメント

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> Sample value: "0-10" </li> <li> **Description:**<br/> The interval that describes the part of the content that has been viewed (in minutes). セグメントは、再生セッション中の再生ヘッドの値の最小値および最大値として計算されます。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツセグメント </li> <li> **Context Data:**<br/> (a.media.segment) </li> <li> **データフィード：**<br/>videosegment </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segment) </li> </ul> |

### コンテンツ名 (変数)

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API キー：**<br/>media.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/>"The Big Bang Theory" </li> <li> **Description:This is the "friendly" (human-readable) name of the content, equal to the last value of In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.**<br/>`s:asset:name.`<br/><br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> ハートビート：(s:asset:name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>コンテンツ名 (変数) </li> <li> ****<br/> コンテキストデータ：(a.media.friendlyName) </li> <li> **データフィード：**<br/>videoname </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### ビデオ名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.name </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：** 1.5.1 </li> <li> **値の例：**<br/>"The Big Bang Theory" </li> <li> ****<br/> 説明：これは、コンテンツの「わかりやすい」（読みやすい）名前で、レポート内の最後の値、ビデオ名は分類、コンテンツ名（変数）は `s:asset:name.`<br/>eVARです。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>friendlyName) </li> <li> ****<br/> ハートビート：(s:asset:name) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ビデオ名 </li> <li> ****<br/> コンテキストデータ：(a.media.friendlyName) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### ビデオパス

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始 </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>"4586695ABC" </li> <li> ****<br/> 説明：サイトやアプリケーション全体のViewerのパスを追跡し、特定のビデオを閲覧するためにViewerがたどったパスを確認できます。 整数と文字の組み合わせになります。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> ハートビート：(s:asset:video_id) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>prop </li> <li> **レポート名：**<br/>ビデオパス </li> <li> ****<br/> コンテキストデータ：(a.media.name) </li> <li> **データフィード：**<br/>videopath </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK バージョン

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API キー：**<br/>media.sdkVersion </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"2.62.0_release" </li> <li> ****<br/> 説明：プレイヤーが使用するSDKバージョン。 プレーヤーに対応する任意のカスタムの値が利用可能です。<br/><br/>レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>sdkVersion) </li> <li> ****<br/> ハートビート：(s:sp:sdk) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.sdkVersion) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL バージョン

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Description: The Media SDK version used for the tracking session. <br/><br/>レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>vhlVersion) </li> <li> ****<br/> Heartbeats: (s:sp:hb_version) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **Context Data:**<br/> (a.media.vhlVersion) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 標準オーディオおよびビデオメタデータ{#section_pfc_hbm_n1b}

### 番組

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SHOW </li> <li> **API キー：**<br/>media.show </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：『モダンファミリー』『ブラックリスト』『新しい少女』 </li> <li> ****<br/> 説明：番組/シリーズ名プ <br/>ログラム名は、番組がシリーズの一部である場合にのみ必要です。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.show) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>番組 </li> <li> ****<br/> コンテキストデータ：(a.media.show) </li> <li> **データフィード：**<br/>videoshow </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.show) </li> </ul> |

### ストリーム形式

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>STREAM_FORMAT </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/>"Live" </li> <li> ****<br/> 説明：ストリームの形式(Live、VOD、Linear)。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.format) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> ****<br/> コンテキストデータ：(a.media.format) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.format) </li> </ul> |

### シーズン

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SEASON </li> <li> **API キー：**<br/>media.season </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値："2” </li> <li> ****<br/> 説明：その番組のシーズン番号。  シーズンシリーズは、番組がシリーズの一部である場合にのみ必要です。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.season) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>シーズン </li> <li> ****<br/> コンテキストデータ：(a.media.season) </li> <li> **データフィード：**<br/>videoseason </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.season) </li> </ul> |

### エピソード

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>EPISODE </li> <li> **API キー：**<br/>media.episode </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値："13" </li> <li> ****<br/> 説明：エピソードの番号。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.episode) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>エピソード </li> <li> ****<br/> コンテキストデータ：(a.media.episode) </li> <li> **データフィード：**<br/>videoepisode </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.episode) </li> </ul> |

### アセット ID

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ASSET_ID </li> <li> **API キー：**<br/>media.assetId </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値："89745363" </li> <li> ****<br/> Description: This is the unique identifier for the content of the media asset, such as the TV series episode identifier, movie asset identifier, or live event identifier. この ID は通常、EIDR、TMS／Gracenote、Rovi などのメタデータを扱う機関から取得します。その他の独自のシステムや社内システムから取得することもできます。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.asset)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>アセット ID </li> <li> ****<br/> Context Data: (a.media.asset) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.asset) </li> </ul> |

### ジャンル

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>GENRE </li> <li> **API キー：**<br/>media.genre </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **Sample value:**<br/> "Drama", "Comedy" </li> <li> **Description:**<br/> Type or grouping of content as defined by content producer. 変数の実装では、値をコンマで区切る必要があります。レポートでは、リスト eVar は各値を行項目に分割し、各行項目は同じ指標の重みを受け取ります。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.genre)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>リスト eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ジャンル </li> <li> ****<br/> コンテキストデータ：(a.media.genre) </li> <li> **データフィード：**<br/>videogenre </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.genre) </li> </ul> |

### 初回放送日

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FIRST_AIR_DATE </li> <li> **API キー：**<br/>media.firstAirDate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> Sample value: "2016-01-25" </li> <li> ****<br/> 説明：コンテンツが最初にテレビで放映された日付。 どのような形式でも問題ありませんが、YYYY-MM-DD の形式にすることをお勧めします。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.airDate)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>初回放送日 </li> <li> ****<br/> コンテキストデータ：(a.media.airDate) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.airDate) </li> </ul> |

### 初回デジタル日

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FIRST_DIGITAL_DATE </li> <li> **API キー：**<br/>media.firstDigitalDate </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> Sample value: "2016-01-25" </li> <li> ****<br/> 説明：任意のデジタルチャネルまたはプラットフォームでコンテンツが最初に放送された日付。 どのような形式でも問題ありませんが、YYYY-MM-DD の形式にすることをお勧めします。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.digitalDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.digitalDate)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>初回デジタル日 </li> <li> ****<br/> コンテキストデータ：(a.media.digitalDate) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### コンテンツ評価

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>RATING </li> <li> **API キー：**<br/>media.rating </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：TVY、TVG、TVPG、TVMA </li> <li> ****<br/> 説明：テレビの保護者によるガイドラインに基づく評価。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>コンテンツ評価 </li> <li> ****<br/> コンテキストデータ：(a.media.rating) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.rating) </li> </ul> |

### 作成者

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>ORIGINATOR </li> <li> **API キー：**<br/>media.originator </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **Sample value:**<br/> "Warner Brothers", "Sony", "Disney" </li> <li> **Description:**<br/> Creator of the content.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.originator) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>作成者 </li> <li> ****<br/> Context Data: (a.media.originator) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.originator) </li> </ul> |

### ネットワーク

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>NETWORK </li> <li> **API キー：**<br/>media.network </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **Sample value:**<br/> "Fox", "Bravo", "ESPN" </li> <li> ****<br/> 説明：ネットワーク/チャネル名。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.network) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>ネットワーク </li> <li> ****<br/> コンテキストデータ：(a.media.network) </li> <li> **データフィード：**<br/>videonetwork </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.network) </li> </ul> |

### 番組タイプ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>SHOW_TYPE </li> <li> **API キー：**<br/>media.showType </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値："0" =全エピソード；"1" =プレビュー/トレーラー；"2" =クリップ；"3" =その他。 </li> <li> ****<br/> 説明：コンテンツのタイプ。0 ～ 3の整数で表します。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.type) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>番組タイプ </li> <li> ****<br/> コンテキストデータ：(a.media.type) </li> <li> **データフィード：**<br/>videoshowtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>MVPD </li> <li> **API キー：**<br/>media.pass.mvpd </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：「Comcast」、「DirecTV」、「Dish」 </li> <li> ****<br/> 説明：アドビ認証を介して提供されたMVPD。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.mvpd) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>MVPD </li> <li> ****<br/> コンテキストデータ：(a.media.pass.mvpd) </li> <li> **データフィード：**<br/>videomvpd </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 認証済み

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>AUTHORIZED </li> <li> **API キー：**<br/>media.pass.auth </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **Sample value:**<br/> "TRUE" </li> <li> ****<br/> 説明：ユーザーはアドビ認証を使用して認証されました。  <br/>**重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.auth) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.pass.<br/>認証) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>認証済み </li> <li> ****<br/> コンテキストデータ：(a.media.pass.auth) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 日パート

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>DAY_PART </li> <li> **API キー：**<br/>media.dayPart </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> **値の例：**<br/> </li> <li> **Description:**<br/> A property that defines the time of the day when the content was broadcast or played. お客様の必要に応じて、任意の値を設定できます。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.dayPart) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>日パート </li> <li> **Context Data:**<br/> (a.media.dayPart) </li> <li> **データフィード：**<br/>videodaypart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### メディアフィードのタイプ

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>FEED </li> <li> **API キー：**<br/>media.feed </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小のSDK のバージョン：** 1.5.7 </li> <li> ****<br/> サンプル値：「East-HD」、「West-HD」、「East-SD」 </li> <li> ****<br/> 説明：フィードのタイプ。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.feed) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>メディアフィードのタイプ </li> <li> ****<br/> コンテキストデータ：(a.media.feed) </li> <li> **データフィード：**<br/>videofeedtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.feed) </li> </ul> |

### 作者名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.artist </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小の** SDKバージョン：1.5.7メディアコレクショ <br/>ンの概 [要またはSDK](/help/media-collection-api/mc-api-overview.md) — バ [ージョン2.2](/help/sdk-implement/download-sdks.md)で入手できます。  </li> <li> **値の例：**<br/>"The Beatles" </li> <li> ****<br/> 説明：アーティストの名前。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.artist) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.artist)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.artist) </li> <li> **データフィード：**<br/>videoaudioartist </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.artist) </li> </ul> |

### アルバム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.album </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小の** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **値の例：**<br/>"Revolver" </li> <li> ****<br/> Description: Name of the album.  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.album) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.album)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.album) </li> <li> **データフィード：**<br/>videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### ラベル

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.label </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小の** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **値の例：**<br/>"Revolver" </li> <li> ****<br/> 説明：レコードのラベルの名前。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.label) </li> <li> **データフィード：**<br/>videoaudiolabel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### 作成者

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.author </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小の** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **値の例：**<br/>"John Kennedy Toole" </li> <li> ****<br/> 説明：（オーディオブックの）作成者の名前。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.author)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.author) </li> <li> **データフィード：**<br/>videoaudioauthor </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.author) </li> </ul> |

### ステーション

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.station </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小の** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **値の例：**<br/>"NPR" </li> <li> ****<br/> 説明：ラジオ局の名前/ID。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.station) </li> <li> **データフィード：**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.station) </li> </ul> |

### 発行者

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.publisher </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディア開始、メディア終了 </li> <li> **最小の** SDKバージョン：1.5.7メディアコレクショ <br/>ンの概 [要またはSDK](/help/media-collection-api/mc-api-overview.md) — バ [ージョン2.2](/help/sdk-implement/download-sdks.md)で入手できます。  </li> <li> **値の例：**<br/>"Random Bauhaus" </li> <li> ****<br/> 説明：オーディオコンテンツの投稿者の名前。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.publisher) </li> <li> ****<br/> ハートビート：(s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/> </li> <li> ****<br/> コンテキストデータ：(a.media.publisher) </li> <li> **データフィード：**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.publisher) </li> </ul> |

## オーディオおよびビデオ指標 {#section_3D5F9C555274428AA6030D07596177E9}

### メディア開始

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定</li> <li> **API キー：**<br/>なし</li> <li> **型：**<br/>文字列</li> <li> ****<br/> 送信先：メディア開始</li> <li> **最小のSDK のバージョン：**&#x200B;すべて可</li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：メディアの読み込みイベント。 （ユーザーが&#x200B;_再生_&#x200B;ボタンをクリックしたときに発生します）。プリロール広告やバッファリング、エラーなどがあった場合でもカウントされます。<br/>**重要：**&#x200B;設定されている場合は true のみを返します。If it is not set, no value is returned.  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.view) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=start) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **Report Name:**<br/> Media Starts </li> <li> ****<br/> Context Data: (a.media.view) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### コンテンツ開始

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **Description:**<br/> First frame of media is consumed. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ開始 </li> <li> ****<br/> コンテキストデータ：(a.media.play) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.play) </li> </ul> |

### コンテンツ完了 {#content-complete}

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：完了まで視聴されたストリーム。 これは、ユーザがストリーム全体を視聴したり、聞いたりしたことを意味するわけではありません。彼らは先に飛び越えたかもしれない これは、ユーザーがストリームの最後(100%)に到達したことを意味します。 <br/>「 [Session End」も参照](quality-parameters.md#session-end) 。 <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> ****<br/> ハートビート：(s:event:<br/>type=complete) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ完了 </li> <li> ****<br/> コンテキストデータ：(a.media.complete) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.complete) </li> </ul> |

### コンテンツ視聴時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：105 </li> <li> ****<br/> 説明：メインコンテンツでPLAYタイプのすべてのイベントのイベント時間（秒）を合計します。  Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ視聴時間 </li> <li> ****<br/> コンテキストデータ：(a.media.timePlayed) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### メディア視聴時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：120 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY, both main and ad content.  Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>メディア視聴時間 </li> <li> **Context Data:**<br/> (a.media.totalTimePlayed) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### ユニーク再生時間

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：94 </li> <li> **Description:**<br/> The value in seconds of the unique segments of content played during a session. 視聴者がコンテンツの同じセグメントを複数回視聴しているシークバックシナリオでの再生時間を除外します。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。  <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>カスタム </li> <li> ****<br/> コンテキストデータ：(a.media.uniqueTimePlayed) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10 %プログレスマーカー

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：再生ヘッドは、長さに基づいてコンテンツの10%マーカーを渡します。 巻き戻しのシークがあった場合でも、このマーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>10％プログレスマーカー </li> <li> ****<br/> コンテキストデータ：(a.media.progress10) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25%プログレスマーカー

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：再生ヘッドは、コンテンツの長さに基づいて、コンテンツの25%マーカーを渡します。 巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>25％プログレスマーカー </li> <li> ****<br/> コンテキストデータ：(a.media.progress25) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50 %プログレスマーカー

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：再生ヘッドは、コンテンツの長さに基づいて、コンテンツの50%マーカーを渡します。 巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>50％プログレスマーカー </li> <li> ****<br/> コンテキストデータ：(a.media.progress50) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75%プログレスマーカー

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> **該当なし** </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 75% marker of content based on content length. 巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>75％プログレスマーカー </li> <li> **Context Data:**<br/> (a.media.progress75) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95%プログレスマーカー

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：再生ヘッドは、コンテンツの長さに基づいてコンテンツの95%マーカーを渡します。 巻き戻しのシークがあった場合でも、マーカーは 1 回のみカウントされます。早送りのシークがあった場合は、スキップされたマーカーはカウントされません。  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>95％プログレスマーカー </li> <li> ****<br/> コンテキストデータ：(a.media.progress95) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress95) </li> </ul> |

### 分平均オーディエンス

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>1 以上 </li> <li> ****<br/> 説明：分平均オーディエンス指標は、1つの特定のメディア項目に関する合計コンテンツ滞在時間を、すべての再生セッションの長さで割って計算されます。 <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>分平均オーディエンス </li> <li> ****<br/> コンテキストデータ：(a.media.averageMinuteAudience) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### フェデレーテッドデータ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> ****<br/> タイプ：boolean </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：true  </li> <li> ****<br/> 説明：ヒットがフェデレーションされる（つまり、顧客が独自の実装ではなく、フェデレーションされたデータ共有の一部として受け取る）場合は、trueに設定します。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>なし </li> <li> ****<br/> コンテキストデータ：(a.media.federated) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.federated) </li> </ul> |

### 推定ストリーム

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> サンプル値：1 - 19分間の再生。 <br/>2 - 31分間の再生。 <br/>3 - 78分間の再生。 </li> <li> **Description:**<br/> The estimated number of video or audio streams per each individual content. コンテンツと広告を含む再生時間 30 分ごとに増加します。レポートでこの値を参照できるようにするためには、独自の処理ルールを作成する必要があります。<br/><br/>A stream is counted every 30 minutes, based on the `ms_s` (or totalTimePlayed = Video Total Time), similar to: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> **Context Data:**<br/> (a.media.estimatedStreams) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### 一時停止の影響を受けたストリーム

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **値の例：**<br/>TRUE </li> <li> **Description:**<br/> This value is either true or false. It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> ****<br/> ハートビート：(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止の影響を受けたストリーム </li> <li> ****<br/> コンテキストデータ：(a.media.pause) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pause) </li> </ul> |

### 一時停止イベント

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> ****<br/> サンプル値：2 </li> <li> ****<br/> 説明：この指標は、再生セッション中に発生した一時停止期間の数として計算されます。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> ****<br/> ハートビート：(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止イベント </li> <li> ****<br/> コンテキストデータ：(a.media.pauseCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 一時停止時間合計

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> ****<br/> サンプル値：190 </li> <li> **Description:**<br/> Sums the duration (in seconds) of all events of type PAUSE. Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。 <br/> **リリース日：2018 年 9 月 14 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>一時停止時間合計 </li> <li> ****<br/> コンテキストデータ：(a.media.pauseTime) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### コンテンツ再開

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/> **media.resume** </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：** 1.5.6 </li> <li> **値の例：**<br/>TRUE </li> <li> **Description:**<br/> A Resume is counted for each playback that resumes after more than 30 minutes of buffer, pause, or stall period OR if this value is set by the player on the VideoInfo trackPlay. <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツ再開 </li> <li> **Context Data:**<br/> (a.media.resume) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.resume) </li> </ul> |

### コンテンツセグメント視聴回数

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> **値の例：**<br/>TRUE </li> <li> ****<br/> 説明：メインコンテンツの表示回数。 A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要：**&#x200B;設定されている場合は true のみを返します。設定されていない場合は値は返されません。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名：**<br/>コンテンツセグメント視聴回数 </li> <li> ****<br/> コンテキストデータ：(a.media.segmentView) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### 広告数

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> ****<br/> SDKキー：該当なし </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> Sample value: 2 </li> <li> ****<br/> Description: The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> ****<br/> Context Data: (a.media.adCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> ****<br/> SDKキー：該当なし </li> <li> **API キー：**<br/>なし </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：メディアを閉じる </li> <li> **最小のSDK のバージョン：**&#x200B;すべて可 </li> <li> ****<br/> Sample value: 2 </li> <li> ****<br/> Description: The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics：**<br/>なし </li> <li> **ハートビート：**<br/>なし </li> </ul> | <ul> <li> **利用可能：**<br/>カスタムの処理ルールを使用 </li> <li> **予約変数：**<br/>なし </li> <li> **レポート名：**<br/>カスタム </li> <li> ****<br/> Context Data: (a.media.chapterCount) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## California Consumer Privacy Act (CCPA) Parameters {#ccpa-params}

### Opt Out Server Side Forwarding

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> ****<br/> SDKキー：該当なし </li> <li> ****<br/> API Key: analytics.optOutServerSideForwarding </li> <li> **必須：**<br/>いいえ </li> <li> ****<br/> タイプ：boolean </li> <li> ****<br/> Sent with: Media Start </li> <li> **最小の** SDKバージョン：該当なし </li> <li> ****<br/> サンプル値：true </li> <li>****<br/> 説明：エンドユーザーがAdobe Analyticsと他のExperience cloudソリューション（Audience Managerなど）との間で共有されるデータをオプトアウトした場合は、trueに設定します。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.dmp) </li> <li> ****<br/> ハートビート：(s:meta:cm.ssf) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> ****<br/> コンテキストデータ：該当なし </li> <li> **データフィード：**<br/>video </li> <li> ****<br/> Audience Manager:該当なし </li> </ul> |

### 共有のオプトアウト

|   実装   | Network Parameters | レポート |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK Key: N/A </li> <li> ****<br/>  APIキー：analytics.optOutShare </li> <li> **必須：**<br/>いいえ </li> <li> ****<br/> タイプ：boolean </li> <li> ****<br/> 送信先：メディア開始 </li> <li> **最小の** SDKバージョン：該当なし </li> <li> **Sample value:**<br/> true </li> <li>****<br/> 説明：エンドユーザーがフェデレーション対象のデータ（他のAdobe Analyticsクライアントなど）をオプトアウトした場合は、trueに設定します。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.oos) </li> <li> ****<br/> ハートビート：(s:meta:cm.oos) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>訪問時 </li> <li> **レポート名：**<br/>コンテンツ </li> <li> ****<br/> コンテキストデータ：該当なし </li> <li> **データフィード：**<br/>video </li> <li> ****<br/> Audience Manager:該当なし </li> </ul> |

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

