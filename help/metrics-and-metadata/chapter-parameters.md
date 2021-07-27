---
title: チャプターパラメーター
description: 実装、ネットワークおよびレポートのチャプターパラメーターについて説明します。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '1067'
ht-degree: 100%

---

# チャプターパラメーター{#chapter-parameters}

このトピックでは、コンテキストデータ値など、アドビがソリューション変数を通じて収集するチャプターおよびセグメントデータのリストを示します。

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

## チャプターメタデータ {#chapter-metadata}

### チャプター名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/> media.chapter.friendlyName </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター開始、チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **説明：**<br/>&#x200B;チャプターまたはセグメントの名前。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>friendlyName） </li> <li> **ハートビート：**<br/>（s:stream:chapter_name） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;デフォルトで作成...  </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;チャプター名 </li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>friendlyName） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>friendlyName） </li> </ul> |

### チャプター位置

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/> media.chapter.index </li> <li> **必須：**<br/> SDK：いいえ、API：はい。 </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/> 2 </li><li> **説明：**<br/>&#x200B;コンテンツ内のチャプターの位置（インデックス、整数）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>position） </li> <li> **ハートビート：**<br/>（l:stream:chapter_pos） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;チャプター位置 </li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>position） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>position） </li> </ul> |

### チャプターオフセット

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/> media.chapter.offset </li> <li> **必須：**<br/> SDK：いいえ、API：はい。 </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/> 58 </li><li> **説明：**<br/>&#x200B;開始時からのコンテンツ内のチャプターのオフセット（秒）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>offset） </li> <li> **ハートビート：**<br/>（l:stream:chapter_offset） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;チャプターオフセット </li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>offset） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>offset） </li> </ul> |

### チャプターの長さ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/> media.chapter.length </li> <li> **必須：**<br/> SDK：いいえ、API：はい。 </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/> 486 </li><li> **説明：**<br/>&#x200B;チャプターの長さ（秒）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>length） </li> <li> **ハートビート：**<br/>（l:stream:chapter_length） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;分類 </li> <li> **レポート名：**<br/>&#x200B;チャプターの長さ </li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>length） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>length） </li> </ul> |

### チャプター

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定 </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;いいえ </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;自動生成されたチャプターの ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>name） </li> <li> **ハートビート：**<br/>（s:stream:chapter_id） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/> eVar </li> <li> **有効期限：**<br/>&#x200B;ヒット時 </li> <li> **レポート名：**<br/>&#x200B;チャプター </li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>name） </li> <li> **データフィード：**<br/> videochapter </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>name） </li> </ul> |

## チャプター指標 {#chapter-Metrics}

### チャプター開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定  </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター開始 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/> TRUE </li><li> **説明：**<br/>&#x200B;開始したチャプターの数。**重要：** このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>view） </li> <li> **ハートビート：**<br/>（s:event:<br/>type=chapter_start） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;チャプター開始</li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>view） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>view） </li> </ul> |

### チャプター完了

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定  </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;文字列 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3</li> <li> **値の例：**<br/> TRUE </li><li> **説明：**<br/>&#x200B;完了したチャプターの数。**重要：** このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>complete） </li> <li> **ハートビート：**<br/>（s:event:<br/>type=chapter_complete） </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;チャプター完了</li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>complete） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>complete） </li> </ul> |

### チャプター閲覧時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>&#x200B;自動設定  </li> <li> **API キー：**<br/>&#x200B;なし </li> <li> **必須：**<br/>&#x200B;はい </li> <li> **型：**<br/>&#x200B;数値 </li> <li> **送信タイミング：**<br/>&#x200B;チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **値の例：**<br/>  </li><li> **説明：**<br/>&#x200B;チャプターの閲覧時間。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 13 日**   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>（a.media.chapter.<br/>timePlayed） </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>&#x200B;可 </li> <li> **予約変数：**<br/>&#x200B;イベント </li> <li> **レポート名：**<br/>&#x200B;チャプター閲覧時間</li> <li> **コンテキストデータ：**<br/>（a.media.chapter.<br/>timePlayed） </li> <li> **データフィード：**<br/>&#x200B;なし </li> <li> **Audience Manager：**<br/>（c_contextdata.<br/>a.media.chapter.<br/>timePlayed） </li> </ul> |

## 関連する API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
