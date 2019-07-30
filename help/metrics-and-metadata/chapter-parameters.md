---
seo-title: チャプターパラメーター
title: チャプターパラメーター
uuid: 2a6b9247- a694-46e9-98e1-424c08c27EC2
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
>"Reporting/Reserved Variable"で説明されている変数の分類名は、「分類」として変更しないでください。\
>メディア分類は、レポートスイートがメディアトラッキングに対して有効になっているときに定義されます。アドビでは、随時、新しいプロパティを追加し、これが発生すると、レポートスイートを再度有効にして、新しいメディアプロパティにアクセスできるようにする必要があります。アドビの更新プロセス中に、変数の名前をチェックすることで、分類が有効かどうかを判定します。見つからない場合は、見つからないものが再度追加されます。

## チャプターメタデータ {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### チャプター名

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.friendlyName </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> チャプター開始、チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> "Big Ban Chapter2- Dearting" </li><li> **説明:**<br/>チャプターまたはセグメントの名前。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>friendlyName） </li> <li> **ハートビート:**<br/> （s:stream:chapter_ name） </li> </ul> | <ul> <li> **利用可能：**<br/>デフォルトで作成...  </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプター名 </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>friendlyName） </li> <li> **データフィード：**<br/>なし </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>friendlyName） </li> </ul> |

### チャプター位置

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.index </li> <li> **必須:**<br/> SDK:いいえ;API:はい。 </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> 2 </li><li> **説明:**<br/>コンテンツ内のチャプターの位置（インデックス、整数）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>position) </li> <li> **ハートビート:**<br/> （l:stream:chapter_ pos） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプター位置 </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>position) </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>position) </li> </ul> |

### チャプターオフセット

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API キー：**<br/>media.chapter.offset </li> <li> **必須:**<br/> SDK:いいえ;API:はい。 </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> 58 </li><li> **説明:**<br/>開始からのコンテンツ内のチャプターのオフセット（秒単位）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>offset） </li> <li> **ハートビート:**<br/> （l:stream:chapter_ offset） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプターオフセット </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>offset） </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>offset） </li> </ul> |

### チャプターの長さ

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/> </li> <li> **API キー：**<br/>media.chapter.length </li> <li> **必須:**<br/> SDK:いいえ;API:はい。 </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> 486 </li><li> **説明:**<br/>チャプターの長さ（秒単位）。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>length) </li> <li> **ハートビート:**<br/> （l:stream:chapter_ length） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>分類 </li> <li> **レポート名：**<br/>チャプターの長さ </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>length) </li> <li> **データフィード：**<br/> </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>length) </li> </ul> |

### チャプター

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定 </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>いいえ </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>自動生成されたチャプターのID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>name) </li> <li> **ハートビート:**<br/> （s:stream:chapter_ id） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>eVar </li> <li> **有効期限：**<br/>ヒット時 </li> <li> **レポート名：**<br/>チャプター </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>name) </li> <li> **データフィード：**<br/>videochapter </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>name) </li> </ul> |

## チャプター指標 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### チャプター開始

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信タイミング：**<br/>チャプター開始 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>開始するチャプターの数。**重要：**&#x200B;このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>view) </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= chapter_ start） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名:**<br/> チャプター開始g </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>view) </li> <li> **データフィード：**<br/>videochapterstart </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>view) </li> </ul> |

### チャプター完了

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>文字列 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3</li> <li> **サンプル値:**<br/> TRUE </li><li> **説明:**<br/>完了したチャプターの数。**重要：**&#x200B;このイベントを設定すると、値は TRUE のみになります。このイベントを設定しない場合は、値が送信されません。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>complete) </li> <li> **ハートビート:**<br/> （s:イベント:<br/>type= chapter_ complete） </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名:**<br/> チャプター完了g </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>complete) </li> <li> **データフィード：**<br/>videochaptercomplete </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>complete) </li> </ul> |

### チャプター閲覧時間

|   実装   | ネットワークパラメーター | レポート |
| --- | --- | --- |
| <ul> <li> **SDK キー：**<br/>自動設定  </li> <li> **API キー：**<br/>なし </li> <li> **必須：**<br/>はい </li> <li> **型：**<br/>数値 </li> <li> **送信先:**<br/> チャプター終了 </li> <li> **最小のSDK のバージョン：** 1.3 </li> <li> **サンプル値:**<br/> </li><li> **説明:**<br/>チャプターの滞在時間。Analysis Workspace と Reports &amp; Analytics では、値は時刻形式（HH:MM:SS）で表示されます。データフィード、Data Warehouse およびレポート API では、値は秒単位で表示されます。<br/>**リリース日：2018 年 9 月 14 日**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> （a. media. chapter.<br/>TimePlayed） </li> <li> **ハートビート：**<br/> </li> </ul> | <ul> <li> **利用可能：**<br/>可 </li> <li> **予約変数：**<br/>イベント </li> <li> **レポート名:**<br/> チャプター滞在時間g </li> <li> **コンテキストデータ:**<br/> （a. media. chapter.<br/>TimePlayed） </li> <li> **データフィード：**<br/>videochaptertime </li> <li> **Audience Manager:**<br/> （c_ contextdata.<br/>a. media. chapter.<br/>TimePlayed） </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
