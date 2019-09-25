---
seo-title: マイルストーンの概要
title: マイルストーンの概要
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356cc5
translation-type: tm+mt
source-git-commit: 7eb14c8e4da742fb426a6e5d0d60ebf8c2063bb6

---


# マイルストーンの概要{#milestone-overview}

>[!CAUTION]
>
>この測定オプションは廃止されました。

[レガシーのマイルストーンドキュメント](milestone_analytics_video.pdf)

## 設定 {#section_rzx_j1z_cfb}

### マイルストーンビデオの設定

ビデオを追跡するには、追跡とレポートに使用される&#x200B;*カスタムコンバージョン変数*（eVar）と&#x200B;*カスタムイベント*&#x200B;のセットを指定します。また、1 つの&#x200B;*カスタムインサイト*&#x200B;変数（）もパスに使用されます。`s.prop`

それぞれの指標に対して選択した変数がビデオ設定ページに追加されます。これにより、システムは、自動的に標準ビデオレポートを生成し、書式設定します。*ビデオ名* eVar と&#x200B;*ビデオビュー*&#x200B;カウンターの両方が必要です。その他の変数は任意ですが、完全な測定をおこなううえで推奨されます。ビデオ追跡を有効にしたら、ビデオ追跡を使用してレポートしたビデオデータから生成されたレポートを表示できます。

さらに、ビデオに関する任意の数の追加指標を追跡できます。例えば、サイトで複数のビデオプレーヤーを使用している場合は、eVar にプレーヤー名を格納できます。選択した変数のいくつかは、サイトの他の領域でも使用される場合があります。例えば、サイト全体で使用される&#x200B;*コンテンツタイプ*&#x200B;変数を利用すると、ビデオから取得されたページ表示の割合を測定したり、コンバージョンイベントをビデオに関連付けたりできます。

### マイルストーンレポートの設定

To set-up video reporting for a Milestone implementation, go to **[!UICONTROL Admin &gt; Report Suite Manager].** レポートスイートを選択し、ビデオ管理/ビ **[!UICONTROL デオレポートを選択します]。**

<!--![](assets/0clip_image002_1537416456.png){width="248"}-->
![](assets/rs1.png)

最初の画面では、マイルストーンデータと共に使用できるのはビデオコアのみです。「**[!UICONTROL ビデオコア]**」を選択し、「**[!UICONTROL 保存]」を選択します。**

![](assets/video-core-check.png)

On the next screen, select **[!UICONTROL Use Custom Variables].**

<!--![](assets/0clip_image006_-1561510960.png){width="470"}-->
![](assets/rs2.png)

最後の画面で、次のように、ビデオ測定で使用する 2 つの eVar と 3 つのイベントを選択します。

<!--![](assets/0clip_image008_-92166399.png)-->
![](assets/rs3.png)

## ビデオ変数リファレンス {#section_emg_c1z_cfb}

次の表に、ビデオのコマース変数とカスタムイベントの詳細を示します。

| ビデオ指標 | 変数の種類 | 説明 |
| --- | --- | --- |
| コンテンツ | eVar <br/>Default expiration:訪問 | （必須）実装での指定に従って、ビデオの名前を収集します。 |
| コンテンツタイプ | eVar <br/>Default expiration: Page view | 訪問者によって閲覧されたコンテンツのタイプに関するデータを収集します。ビデオ測定によって送信されたヒットには、コンテンツタイプが割り当て `video.` ら <br/>れます。この変数は、ビデオトラッキング専用に予約する必要はありません。 この同じ変数を使用する他のコンテンツレポートコンテンツタイプを使用すると、異なるタイプのコンテンツに対する訪問者の分布を分析できます。 For example, you could tag other content types using values such as `article` or `product page` using this variable. <br/>ビデオ測定の見地からすると、*コンテンツタイプ*&#x200B;を使用することによってビデオ訪問者を識別でき、その結果、ビデオのコンバージョン率を計算できます。 |
| コンテンツ視聴時間 | Event <br/>Type: Counter | 前回のデータ収集プロセス（イメージリクエスト）以降のビデオ視聴秒数をカウントします。 |
| ビデオ開始 | Event <br/>Type: Counter | 訪問者がビデオの一部を視聴したことを示します。ただし、訪問者がビデオを視聴した時間や視聴した部分に関する情報は提供されません。 |
| ビデオ完了 | event <br/>タイプ：カウンター | ユーザーがビデオを最後まで視聴したことを示します。デフォルトでは、完了イベントはビデオが終了する 1 秒前に測定されます。<br/>導入時に、表示完了と見なすビデオの終わりからの秒数を指定できます。終わりが定義されないライブビデオやその他のストリーミングの場合は、完了を測定するためのカスタムポイントを指定できます。例えば、表示開始から特定の時間が経過したポイントなどです。 |

## メディアモジュール変数 {#section_ts5_11z_cfb}

次の変数を使用して、ビデオ測定を設定できます。「必須変数」の表に示した変数に対する値を定義する必要があります。また、ビデオプレーヤーでイベントを追跡するには、autoTrack を有効にするか（サポートされているプレーヤーの場合）、open、play、stop および close の各メソッドを使用してカスタムプレーヤーイベント追跡を導入する必要があります。

| 変数    | 説明 |
| --- | --- |
| `Media.trackUsingContextData` | **構文：**<br/><br/> `s.Media.trackUsingContextData = true;`<br/>このオプションは、統合ビデオ追跡を有効にします。trueに設定した場合、メディアモジュールは、レガシーデータではなく、メディアトラッキング用のコンテキストデータを生成しま `pev3`す。 <br/>`Media.contextDataMapping` を使用して、選択した eVar および event にコンテキストデータをマッピングします。<br/>デフォルト値： `false` |
| `Media.contextDataMapping` | **構文：**<br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};`<br/><br/>ビデオ測定に使用する eVar および event への変数マッピングを定義するオブジェクトです。The object must map the following fields: <br/><br/> **a.media.name：**（必須）変数にビデオ名を入力します。ビデオ名の格納先として選択した eVar と、ビデオパス用に使用するカスタムインサイトビデオ変数（`s.prop`）を指定します。Provide the values in a comma-separated list. <br/><br/> **a.media.segment：**（オプション）メディアセグメント名の格納先の eVar です。a.contentType：（オプション）ビデオ値の格納先の eVar。これには、ビデオの訪問回数および訪問者数のレポート生成が有効にされた、訪問回数および訪問者数の追跡機能が含まれます。選択する変数は、記事、スライドショー、製品ページというように、データの格納に既に使用されているものの場合もあります。<br/><br/> **** a.media.view:（必須）メディアビューをカウントするイベント。 <br/><br/> **** a.media.segmentView:（オプション）セグメントビューをカウントするイベント。 <br/><br/> **** a.media.complete:（オプション）完全なビューをカウントするイベント。 <br/><br/> **** a.media.timePlayed:（オプション、強く推奨）再生されたビデオの秒数を格納する数値イベント。 <br/><br/> **a.media.milestones：**（オプション）s.Media.trackMilestones マイルストーンをカウンターイベントにマッピングするオブジェクトです。マイルストーンを定義する場合は、Media.segmentByMilestones を true に設定する必要があります。 <br/><br/> **広告トラッキング** ：広告をトラッキングするには、以下のコンテキストデータ変数を使用できます。 <br/> **a.media.ad.name：**（必須）変数に広告名を入力します。広告名の格納先として選択した eVar と、パス用に使用するカスタムインサイトビデオ変数（`s.prop`）を指定します。Provide the values in a comma-separated list. <br/><br/> **** a.media.ad.pod:広告が再生されたプライマリコンテンツ内の位置。 <br/><br/> **** a.media.ad.podPosition:広告が表示されるポッド内の位置。 <br/><br/> **** a.media.ad.CPM:この再生に適用されるCPMまたは暗号化されたCPM（「～」のプリフィックスが付く）。 <br/><br/> **a.media.ad.view：** と同じように機能します。`a.media.view`<br/><br/> **** a.media.ad.clicked:広告のクリック数をカウント(呼び出し`Media.click` ) <br/><br/> **a.media.ad.timePlayed：** と同じように機能します。`a.media.timePlayed`<br/><br/> **** a.media.ad.complete:a.media.ad.segmentと同じように機能 `a.media.complete` します。次と同じように機能しま `a.media.segment` す <br/><br/> **a.media.ad.segmentView：** と同じように機能します。`a.media.segmentView`<br/><br/> **a.media.ad.milestones：** と同じように機能します。`a.media.milestones`<br/><br/> **a.media.ad.offsetMilestones：** と同じように機能します。`a.media.offsetMilestones` |
| `Media.trackVars` | **構文：**<br/><br/> `s.Media.trackVars =` <br/>    `"events,` `prop2,` `eVar1,` `eVar2,` `eVar3";` <br/><br/>A comma-separated list of all variables that are set in your video tracking code. |
| `Media.trackEvents` | **構文：**<br/><br/> `s.Media.trackEvents =` <br/>    `"event1,` `event2,` `event3,` `event4,` `event5,` `event6,` `event7"` <br/><br/>A comma-separated list of all events that are set in your video tracking code. |

## オプションの変数 {#section_ufg_zzy_cfb}

|  変数    | 説明 |
| --- | --- |
| `Media.autoTrack` | **構文：**<br/><br/> `s.Media.autoTrack = true`<br/><br/>サポートされているプレーヤーの自動追跡を有効にします。サポートされているプレーヤーは次のとおりです。 <ul> <li> Open Source Media Framework（OSMF） </li> <li> FLVPlayback（Flash Professional のビデオのインポートウィザードによって作成されるビデオプレーヤー） </li> <li> Silverlight </li> <li> MediaDisplay </li> <li> MediaPlayback </li> <li> Brightcove API バージョン 2 および 3（[Brightcove](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_other_players.html) を参照） </li> <li> JavaScript を使用する、Windows Media Player、Quicktime または Real Player </li> </ul> <br/><br/>上記のプレーヤーの1つを使用しない場合は、プレーヤーイベントの追跡に `Media.open``Media.play``Media.stop``Media.close` を使用できます。 |
| `Media.autoTrackNetStreams` | **構文：**<br/><br/> `s.Media.autoTrackNetStreams = true`<br/><br/>Flash 10.3 では、拡張ビデオ追跡を可能にする新しい機能が NetStream コンポーネントに追加されました。カスタム Flash NetStream プレーヤーを使用する場合は、この変数を有効にすることで、autoTrack と同様の機能を有効にできます。このメソッドを使用するには、ビデオが Flash 10.3 以降で視聴されている必要があります。 |
| `Media.completeByCloseOffset` | **構文：**<br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true`<br/><br/>この設定を使用すると、実際にビデオの最後に到達する数秒前に、ビデオビューの完了としてカウントできます。<br/><br/>イベントは、`completeCloseOffsetThreshold` で指定されている秒数に基づいて送信されます。これにより、ビデオの長さに等しいオフセットの報告を実行しないビデオプレーヤーでも、完了を測定できます。<br/><br/>デフォルトでは、この値は true に設定され、しきい値は 1 秒に設定されます。これらのデフォルトでは、完了イベントは、ビデオの最後の 1 秒前に送信されます。 |
| `Media.completeCloseOffsetThreshold` | **構文：**<br/><br/> `s.Media.completeCloseOffsetThreshold = 1`<br/><br/>このしきい値を使用すると、実際にビデオの最後に到達する数秒前に、ビデオビューの完了としてカウントできます。このしきい値を使用するには、`Media.completeByCloseOffset` を true に設定する必要があります。<br/><br/>指定する整数値によって、close 時に完了としてカウントされる、ビデオの長さからのオフセットの値（秒数）が決まります。これにより、ビデオの長さに等しいオフセットの報告を実行しないビデオプレーヤーでも、完了を測定できます。<br/><br/>しきい値のデフォルトは 1 秒です。 |
| `Media.playerName` | **構文：**<br/><br/> `s.Media.playerName = "Custom Player Name"`<br/><br/>カスタムビデオプレーヤー名を指定します。 |
| `Media.trackSeconds` | **構文：**<br/><br/> `s.Media.trackSeconds = 15`<br/><br/>ビデオ再生中にビデオ追跡データを Adobe データ収集サーバーへ送信する時間間隔を秒数で定義します。値は 5 秒単位の増分で設定する必要があります。<br/><br/> を有効に `Media.trackSeconds` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、Media.Monitor を使用する必要があります。 |
| `Media.trackMilestones` | Tracks milestones as percentage of the video length.  <br/><br/> **構文：**<br/><br/> `s.Media.trackMilestones = "25, 50, 75";`<br/><br/>ビデオ追跡データを Adobe データ収集サーバーに送信する時間間隔を、ビデオの長さの割合として定義します。整数のコンマ区切りリストとしてマイルストーンを指定します。例えば、10 は 10％を表し、23 は 23％を表します。<br/><br/>これらのマイルストーンはビデオ内の固定ポイントなので、訪問者が 10％のマイルストーンをまたいで視聴し、その後に巻戻しを実行して、もう一度 10％のマイルストーンを通過した場合、メディアモジュールは追跡データを複数回送信します。同様に、ある訪問者が早送りしてマイルストーンを通過した場合、そのマイルストーンについての追跡データはメディアモジュールによって送信されません。<br/><br/>を有効に `Media.trackMilestones` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、Media.Monitor を使用する必要があります。 |
| `Media.trackOffsetMilestones` | Tracks milestones as seconds elapsed from the beginning of the video.  <br/><br/> **構文：**<br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";`<br/><br/>ビデオ追跡データを Adobe データ収集サーバーに送信する時間間隔を、ビデオの開始時点からの経過秒数として定義します。整数のコンマ区切りリストとしてマイルストーンを指定します。例：20 = 20 秒、40 = 40 秒。<br/><br/>これらのマイルストーンはビデオ内の固定ポイントなので、訪問者が 20 秒のマイルストーンをまたいで視聴し、その後に巻戻しを実行して、もう一度 20 秒のマイルストーンを通過した場合、メディアモジュールは追跡データを複数回送信します。同様に、ある訪問者が早送りしてマイルストーンを通過した場合、そのマイルストーンについての追跡データはメディアモジュールによって送信されません。<br/><br/> を有効に `Media.trackOffsetMilestones` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、Media.Monitor を使用する必要があります。 |
| `Media.segmentByMilestones` | **構文：**<br/><br/> `s.Media.segmentByMilestones = true;` メディ <br/><br/>アの長さと、マイルストーンによるセグメント化で指定されたマイルストーンに基づいて、セグメント名、セグメント番号およびセグメントの長さのデータを自動的に生成します。 `Media.trackMilestones`<br/><br/>これは、を使用する場合にセグメントを定義する唯一の方法で `autoTrack`す。 <br/><br/>デフォルト値： `false` |
| `Media.segmentByOffsetMilestones` | **構文：**<br/><br/> `s.Media.segmentByOffsetMilestones = true;` メディ <br/><br/>アの長さと、マイルストーンによるセグメント化で指定されたマイルストーンに基づいて、セグメント名、セグメント番号およびセグメントの長さのデータを自動的に生成します。 `Media.trackOffsetMilestones`<br/><br/>これは、を使用する場合にセグメントを定義する唯一の方法で `autoTrack`す。  <br/><br/>デフォルト値： `false` |

## 広告トラッキング変数 {#section_bhv_xzy_cfb}

これらの変数は、openAd メソッドと組み合わせて広告情報を送信するために使用されます。See [VAST Video Ad Tracking.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_ads.html)

| 変数    | 説明 |
| --- | --- |
| `Media.adTrackSeconds` | **構文：**<br/><br/> `s.Media.adTrackSeconds = 15;`<br/><br/>ビデオ再生中にビデオ広告追跡データを Adobe データ収集サーバーに送信する時間間隔を秒数で定義します。値は 5 秒単位の増分で設定する必要があります。<br/><br/> を有効に `Media.adTrackSeconds` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、`Media.monitor` を使用する必要があります。 |
| `Media.adTrackMilestones` | Tracks ad milestones as percentage of the ad length.  <br/><br/> **構文：**<br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";`<br/><br/>広告追跡データを Adobe データ収集サーバーに送信する時間間隔を、広告の長さの割合として定義します。整数のコンマ区切りリストとしてマイルストーンを指定します。例：10 = 10%、23 = 23%)。  <br/><br/>これらのマイルストーンは広告内の固定ポイントなので、訪問者が 10％のマイルストーンをまたいで視聴し、その後に巻戻しを実行して、もう一度 10％のマイルストーンを通過した場合、メディアモジュールは追跡データを複数回送信します。同様に、ある訪問者が早送りしてマイルストーンを通過した場合、そのマイルストーンについての追跡データはメディアモジュールによって送信されません。<br/><br/> を有効に `Media.adTrackMilestones` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、`Media.monitor` を使用する必要があります。 |
| `Media.adTrackOffsetMilestones` | Tracks ad milestones as seconds elapsed from the beginning of the ad.  <br/><br/> **構文：**<br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";`<br/><br/>広告追跡データを Adobe データ収集サーバーに送信する時間間隔を、広告の開始時点からの経過秒数として定義します。整数のコンマ区切りリストとしてマイルストーンを指定します。例：20 = 20 秒、40 = 40 秒。<br/><br/>これらのマイルストーンは広告内の固定ポイントなので、訪問者が 20 秒のマイルストーンをまたいで視聴し、その後に巻戻しを実行して、もう一度 20 秒のマイルストーンを通過した場合、メディアモジュールは追跡データを複数回送信します。同様に、ある訪問者が早送りしてマイルストーンを通過した場合、そのマイルストーンについての追跡データはメディアモジュールによって送信されません。<br/><br/> を有効に `Media.adTrackOffsetMilestones` すると、で定義されたイベントのみがトリガーされま `Media.contextDataMapping`す。 ビデオ測定のために指定以外の変数を追加で送信するには、`Media.monitor` を使用する必要があります。 |
| `Media.adSegmentByMilestones` | **構文：**<br/><br/> `s.Media.adSegmentByMilestones = true;` メディ <br/><br/>アの長さと、マイルストーンによるセグメント化で指定されたマイルストーンに基づいて、セグメント名、セグメント番号およびセグメントの長さのデータを自動的に生成します。 `Media.adTrackMilestones`<br/><br/>これは、を使用する場合にセグメントを定義する唯一の方法で `autoTrack`す。  <br/><br/>デフォルト値： `false` |
| `Media.adSegmentByOffsetMilestones` | **構文：**<br/><br/> `s.Media.adSegmentByOffsetMilestones = true;` メディ <br/><br/>アの長さと、マイルストーンによるセグメント化で指定されたマイルストーンに基づいて、セグメント名、セグメント番号およびセグメントの長さのデータを自動的に生成します。 `Media.adTrackOffsetMilestones`<br/><br/>これは、を使用する場合にセグメントを定義する唯一の方法で `autoTrack`す。 <br/><br/>デフォルト値： `false` |

## メディアモジュールメソッド {#section_xp1_wzy_cfb}

メディアモジュールメソッドを使用すると、プレーヤーのイベントを手動で追跡したり、標準ビデオレポートに含まれていない追加の指標を追跡したりできます。

`Media.autoTrack` を使用し、追加指標を追跡しない場合、これらのメソッドを直接呼び出す必要はありません。特にオプションとして指定されていない限り、すべての引数が必要です。

| メソッド    | 説明 |
| --- | --- |
| `Media.open` | **構文：**<br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)`<br/><br/>メディアモジュールでビデオトラッキングデータを収集するよう準備します。このメソッドでは次のパラメーターを利用します。 <ul><li> **mediaName：**（必須）ビデオレポートに表示するビデオの名前。 </li><li>  **mediaLength：**（必須）ビデオの長さ（秒単位）。  </li><li> **mediaPlayerName：**（必須）ビデオの視聴に使用されるメディアプレーヤーの名前。ビデオレポートに表示する名前です。 </li></ul> |
| `Media.openAd` | **構文：**<br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>   メデ `parentPod, parentPodPosition, CPM)`<br/><br/>ィアモジュールで広告トラッキングデータを収集するよう準備します。 このメソッドでは次のパラメーターを利用します。 <ul> <li> **name：**（必須）広告の名前または ID。  </li> <li> **length：**（必須）広告の長さ。  </li> <li> **playerName：**（必須）広告の表示に使用するメディアプレーヤーの名前。  </li> <li> **parentName：**&#x200B;広告が埋め込まれたプライマリコンテンツの名前または ID。  </li> <li> **parentPod：**&#x200B;広告が表示されたプライマリコンテンツ内の位置。  </li> <li> **parentPodPosition：**&#x200B;広告が表示されるポッド内の位置。  </li> <li> **CPM：**&#x200B;この再生に適用される CPM または暗号化された CPM（「~」のプレフィックスが付く）。  </li> </ul> |
| `Media.click` | **構文：**<br/><br/> `s.Media.click(name, offset)`<br/><br/>ビデオで広告がいつクリックされたかを追跡します。このメソッドでは次のパラメーターを利用します。 <ul> <li> **name：**&#x200B;広告の名前。Media.openAd で使用されている名前と一致させる必要があります。  </li> <li> **offset：**&#x200B;クリックが発生した際の、広告までのオフセット。  </li> </ul> |
| `Media.close` | **構文：**<br/><br/> `s.Media.close(mediaName)`<br/><br/>ビデオデータの収集を終了して情報を Adobe データ収集サーバーに送信します。このメソッドはビデオの最後で呼び出します。このメソッドでは次のパラメーターを利用します。 <br/><br/> **mediaName：**&#x200B;ビデオ名。`Media.open` で使用されている名前と一致させる必要があります。 |
| `Media.complete` | **構文：**<br/><br/> `s.Media.complete(name, offset)`<br/><br/>このメソッドを使用して、完了イベントを手動で追跡します。このメソッドは、`Media.completeByCloseOffset` で処理できない特別なロジックを使用してイベントをトリガーする必要がある場合に使用します。<br/><br/>例えば、最後が定義されていないライブストリームを測定する場合、ユーザーがライブストリームを X 秒間視聴した後で、完了をトリガーすることができます。コンテンツの長さと種類に基づいた割合の計算を使用して、完了を測定します。このメソッドでは次のパラメーターを利用します。 <ul> <li> **mediaName：**&#x200B;ビデオ名。Media.open で使用されている名前と一致させる必要があります。  </li> <li> **mediaOffset：**&#x200B;完了イベントを送信する、ビデオ開始後の秒数。ゼロ秒を開始点としてオフセットを指定します。<br/><br/>メディアプレーヤーでマイルストーンを使用して追跡を行っている場合は、Media.complete を呼び出す前に、値を秒数に必ず変換してください。  </li> </ul> completeを手動で呼び出す場合は、 <br/><br/> `s.Media.completeByCloseOffset = false` を参照してください。 |
| `Media.play` | **構文：**<br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)`<br/><br/>ビデオの再生を開始するときは常にこのメソッドを呼び出します。手動でビデオ測定を行う場合、ビデオ測定データを送信するときに現在のセグメントデータを送信できます。<br/><br/>プレイヤーがあるセグメントから別のセグメントに変更された場合は、何らかの理由でを呼び出す必要がありま `Media.stop``Media.play`す。 <br/><br/>このメソッドは、次のパラメーターを取ります。 <br/><br/> **mediaName：**&#x200B;ビデオ名。Media.open で使用されている名前と一致させる必要があります。  <br/><br/> **mediaOffset：**&#x200B;ビデオの再生が開始されてからの秒数。ゼロ秒を開始点としてオフセットを指定します。メディアプレーヤーでマイルストーンを使用して追跡を行っている場合は、Media.play を呼び出す前に、値を秒数に必ず変換してください。  <br/><br/> **segmentNum：**（オプション）現在のセグメント番号。マーケティングレポートでは、この番号を使用して、レポートでのセグメントの表示順を決定します。segmentNum には、正の数を指定する必要があります。  <br/><br/> **** セグメント：（オプション）現在のセグメント名。  <br/><br/> **** segmentLength:（オプション） <br/><br/>現在のセグメントの長さ（秒単位）。  <br/><br/>例： <br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **構文：**<br/><br/> `s.Media.stop(mediaName, mediaOffset)`<br/><br/>指定したビデオの停止イベント（停止、一時停止など）を追跡します。このメソッドでは次のパラメーターを利用します。 <ul> <li> **mediaName：**&#x200B;ビデオ名。`Media.open` で使用されている名前と一致させる必要があります。  </li> <li> **mediaOffset：**&#x200B;停止または一時停止が発生するビデオ開始後の秒数。ゼロ秒を開始点としてオフセットを指定します。  </li> </ul> |
| `Media.monitor` | **構文：**<br/><br/> `s.Media.monitor(s, media)` <br/><br/> **Silverlight の構文：**<br/><br/> `s.Media.monitor =` Silverlightア <br/>プリメディアモニ `new AppMeasurement_Media_Monitor(myMediaMonitor);`<br/><br/>ターは、Objective-C delegateのデザインパターンを実装します。 クラスメ `myMediaMonitor` ソッドは、パラメーターとパ `s` ラメーターを `media` 取ります。 <br/><br/>このメソッドを使用して、追加のビデオ指標を送信します。変数（prop、eVar、event）を追加したり、ビデオの再生進行に伴う最新の状態に基づいて `Media.track` を呼び出し、変数を送信したりできます。<br/><br/>Media.monitorを使 [用した追加指標の測定を参照してください。](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) このメソ <br/><br/>ッドは次のパラメーターを取ります。 <br/><br/>  **** s:インス `AppMeasurement` タンス(またはJavaScriptオ `s` ブジェクト)。 <br/><br/> **** media:メンバーがビデオの状態を提供するオブジェクトです。 メンバーの例は次のとおりです。  <ul><li> `media.name:` ビデオの名前。 This must match the name used in `Media.open`; </li><li> `media.length:` への呼び出しで提供されるビデオの長さ（秒） `Media.open`; </li><li> `media.playerName:` への呼び出しで提供されるメディアプレイヤーの名 `Media.open`前。 </li><li> `media.openTime:` いつ呼び出されたかに関するデータを含むNSDate `Media.open` オブジェクト。 </li><li> `media.offset:` ビデオへの現在のオフセット（秒単位、実際のビデオポイント）。 オフセットは0から始まります（ビデオの最初の秒は0秒）。 </li><li> `media.percent:` ビデオの長さと現在のオフセットに基づく、再生されたビデオの現在の割合。;  </li><li> `media.timePlayed:` これまでの再生秒数の合計。  </li><li> `media.eventFirstTime:` このビデオに対してこのメディアイベントが初めて呼び出されたかどうかを示します。 </li><li> `media.mediaEvent:` モニターが呼び出される原因となったイベント名を含む文字列。 </li></ul> |
|  | `media.mediaEvent` events: <ul><li> `OPEN:` 再生が最初に観察される `Media.autoTrack` とき、または呼び `Media.play`出し </li><li> `CLOSE:` ビデオの完了時に再生が終了したとき、または `Media.autoTrack` 次の呼び出し時に終了したとき `Media.close`。</li><li> `PLAY:` 一時停止またはスクラブ後に再生が再開されたとき、 `Media.autoTrack` または2回目の呼び出しを行ったとき `Media.play`。</li><li> `STOP:` スクラブの開始の一時停止またはへの呼び出しによって再生が停 `Media.autoTrack` 止した場合 `Media.stop`。</li><li> `MONITOR:` 自動監視機能が再生中にビデオの状態をチェックするとき（毎秒）。</li><li> `SECONDS:` 変数で定義された2番目の間 `Media.trackSeconds` 隔。</li><li> `MILESTONE:` 変数で定義されたマイルスト `Media.trackMilestones` ーン。 </li></ul> |
| `Media.track` | **構文：**<br/><br/> `s.Media.track(mediaName)`<br/><br/>現在のビデオの状態と共に、ユーザーが定義した `Media.trackVars` と Media.trackEvents を即座に送信します。このメソッドは、`Media.monitor` 内で使用します。<br/><br/>Media.monitorを使 [用した追加指標の測定を参照してください。](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) このメ <br/><br/>ソッドを `Media.open` 呼び出す `Media.play` 前に、ビデオを呼び出します。 このメソッドでは次のパラメーターを利用します。 <ul> <li> **mediaName**：ビデオ名。`Media.open` で使用されている名前と一致させる必要があります。</li> </ul> このメソッドは、ビデオ再生中に他の変数を送信する唯一の方法です。このメソッドは、追跡が複数回ヒットしないように、秒間隔およびパーセントマイルストーンを 0 にリセットします。 |


## ビデオプレーヤーイベントの追跡 {#section_dsg_rzy_cfb}

ビデオプレーヤーのイベントハンドラーに追加する関数を作成することで、メディアプレーヤーを追跡できます。This lets you call `Media.open`, `Media.play`, `Media.stop`, and `Media.close` at the appropriate times. 次に例を示します。

* **** ロード：呼び出し `Media.open` と `Media.play`
* **** 一時停止：呼び出し `Media.stop`ます。 例えば、ユーザーが 15 秒後にビデオを一時停止したときは、`s.Media.stop("Video1", 15)` ) を呼び出します。
* **バッファー：**&#x200B;ビデオのバッファリング中に `Media.stop` を呼び出します。再生の再開時に `Media.play` を呼び出します。
* **** 再開：呼び出し `Media.play`ます。 例えば、ユーザーが最初にビデオを 15 秒間再生した後にビデオを再開した場合は、`s.Media.play("Video1", 15)` を呼び出します。
* **スクラブ（スライダー）：**&#x200B;ユーザーがビデオスライダーをドラッグしたとき、`Media.stop` を呼び出します。ユーザーがビデオのスライダーを離したときに、`Media.play` を呼び出します。
* **** 終了：じゃあ `Media.stop`電話して `Media.close`。 例えば、100 秒のビデオの終了時に、`s.Media.stop("Video1", 100)` を呼び出し、次に `s.Media.close("Video1")` を呼び出します。

以上を実行するために、メディアプレーヤーイベントハンドラーから呼び出すことができる 4 つのカスタム関数を定義します。The various parameters passed into `Media.open`, `Media.play`, `Media.stop`, and `Media.close` come from the player. 次の擬似コードに、この処理を示します。

```javascript
/* Call on video load */ 
function startMovie() { 
    s.Media.open(mediaName, mediaLength, mediaPlayerName); 
    playMovie(); 
} 
 
/* Call on video resume from pause and slider release */ 
function playMovie() { 
    s.Media.play(mediaName, 
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength); 
} 
/* Call on video pause and slider grab */ 
function stopMovie() { 
    s.Media.stop(mediaName, mediaOffset); 
} 
 
/* Call on video end */ 
/* Measuring Video for Developers 43 */ 
function endMovie() { 
    stopMovie(); 
    s.Media.close(mediaName); 
} 
```

## JavaScript autotrack {#section_ahz_pzy_cfb}

The JavaScript media module identifies all `<embed>` or `<object>` tags in the page HTML. その後、各タグのデータを検索し、使用されているメディアプレーヤーがある場合はどのメディアプレーヤーかを判断します。プレーヤーが Windows Media Player、Quicktime、または Real Player の場合は、`autoTrack` を使用できます。ただし、Windows Media Player については、`autoTrack` が機能するのは Internet Explorer のみです。その他のすべてのブラウザーをサポートするには、Windows Media Player の手動の追跡が必要です。

追跡するオブジェクトに `classid` 属性を設定する必要があります。ビデオを自動的に追跡するには、`classid` は、メディアモジュールで使用するイベントハンドラーを公開する必要があります。

```javascript
s.Media.autoTrack = true
```

## JavaScript のサンプルコード {#section_i4g_4zy_cfb}

```javascript
// Sample implementation 
s.usePlugins=true 
function s_doPlugins(s) { 
    /* Add manual calls to modules and plugins here */ 
} 
 
s.doPlugins=s_doPlugins 
 
/*********Media Module Calls**************/ 
s.loadModule("Media") 
 
/*Configure Media Module Functions */ 
s.Media.autoTrack= true; 
s.Media.trackVars="events, prop2, eVar1, eVar2, eVar3"; 
s.Media.trackEvents="event1, event2, event3, event4, event5, event6, event7" 
s.Media.trackMilestones="25, 50, 75"; 
s.Media.playerName="My Media Player"; 
s.Media.segmentByMilestones = true; 
s.Media.trackUsingContextData = true; 
s.Media.contextDataMapping = { 
    "a.media.name":"eVar2, prop2", 
    "a.media.segment":"eVar3", 
    "a.contentType":"eVar1", 
    "a.media.timePlayed":"event3", 
    "a.media.view":"event1", 
    "a.media.segmentView":"event2", 
    "a.media.complete":"event7", 
    "a.media.milestones":{ 
        25:"event4", 
        50:"event5", 
        75:"event6" 
    } 
} 
 
s.Media.monitor = function (s, media) { } //If Needed

/* Turn on and configure debugging here */ 
s.debugTracking = true; 
s.trackLocal = true; 
 
/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor 
data is collected. Changes should only be made when instructed to do so by your account 
manager.*/ 
s.visitorNamespace = "yourNamespace"; 
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies 
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL 
s.dc = '122'; 
 
/************************** PLUGINS SECTION *************************/ 
/* Insert any plugins code you want to use here. */ 
 
/****************************** MODULES *****************************/ 
/* Insert the media module tracking code here. */ 
```

