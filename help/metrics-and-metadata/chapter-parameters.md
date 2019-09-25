---
seo-title: チャプターパラメーター
title: チャプターパラメーター
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# チャプターパラメーター{#chapter-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するチャプターおよびセグメントデータのリストを示します。

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
>「レポート/予約変数」で「分類」として説明されている以下の変数の分類名は変更しないでください。\
>メディア分類は、レポートスイートでメディアの追跡が有効になっている場合に定義されます。 アドビは、新しいプロパティを随時追加し、その場合は、新しいメディアプロパティにアクセスするためにレポートスイートを再度有効にする必要があります。 更新プロセス中に、変数の名前を確認することで、分類が有効かどうかが判断されます。 いずれかが見つからない場合は、見つからないものが再度追加されます。

## チャプターメタデータ {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### チャプター名

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.friendlyName </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：チャプター開始、チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> ****<br/> サンプル値：『ビッグバン第2章 — 年代記』 </li><li> **説明：チ**<br/>ャプターまたはセグメントの名前。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **利用可能：**<br/>デフォルトで作成...  </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプター名 </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>friendlyName) </li> <li> **データフィード：**<br/>なし </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>friendlyName) </li> </ul> |

### チャプター位置

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.index </li> <li> ****<br/> 必須：SDK:いや、API:はい。 </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> ****<br/> サンプル値：2 </li><li> **Description:The position (index, integer) of the chapter inside the content.**<br/>   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>position) </li> <li> ****<br/> ハートビート：(l:stream:chapter_pos) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプター位置 </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>position) </li> <li> **データフィード：**<br/> </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>position) </li> </ul> |

### チャプターオフセット

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.offset </li> <li> ****<br/> 必須：SDK:いや、API:はい。 </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> ****<br/> サンプル値：58 </li><li> **Description:**<br/>The offset of the chapter inside the content (in seconds) from the start.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>オフセット) </li> <li> ****<br/> ハートビート：(l:stream:chapter_offset) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプターオフセット </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>オフセット) </li> <li> **データフィード：**<br/> </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>オフセット) </li> </ul> |

### チャプターの長さ

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.chapter.length </li> <li> ****<br/> 必須：SDK:いや、API:はい。 </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> ****<br/> サンプル値：486 </li><li> **Description:**<br/>The length of the chapter, in seconds.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>length) </li> <li> ****<br/> ハートビート：(l:stream:chapter_length) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプターの長さ </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>length) </li> <li> **データフィード：**<br/> </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>length) </li> </ul> |

### チャプター

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **Sent with:**<br/> Chapter Close </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値：**<br/> </li><li> **説明：**<br/>チャプターの自動生成ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>name) </li> <li> ****<br/> ハートビート：(s:stream:chapter_id) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>チャプター </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>name) </li> <li> **データフィード：**<br/>videochapter </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter<br/>name) </li> </ul> |

## チャプター指標 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### チャプター開始

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>チャプター開始 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> ****<br/> サンプル値：TRUE </li><li> **説明：**<br/>開始するチャプターの数。  **重要：**&#x200B;このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>view) </li> <li> ****<br/> ハートビート：(s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> ****<br/> レポート名：チャプター開始g </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>view) </li> <li> **データフィード：**<br/>videochapterstart </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>view) </li> </ul> |

### チャプター完了

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> ****<br/> 送信先：チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3</li> <li> ****<br/> サンプル値：TRUE </li><li> **Description:The number of chapter completes.**<br/>**重要：**&#x200B;このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>complete) </li> <li> ****<br/> Heartbeat: (s:event:type=chapter_complete)<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> ****<br/> レポート名：チャプター完了g </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>complete) </li> <li> **データフィード：**<br/>videochaptercomplete </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>complete) </li> </ul> |

### チャプター閲覧時間

|   実装   | ネットワークパラメータ | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> ****<br/> 送信先：チャプター閉じる </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値：**<br/> </li><li> **説明：チ**<br/>ャプターでの滞在時間。  Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter)。<br/>timePlayed) </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> ****<br/> レポート名：チャプター滞在時間g </li> <li> ****<br/> コンテキストデータ：(a.media.chapter)。<br/>timePlayed) </li> <li> **データフィード：**<br/>videochaptertime </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter<br/>timePlayed) </li> </ul> |

## 関連API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
