---
title: オーディエンスを新しい Adobe Analytics for Streaming Media データタイプに移行する
description: オーディエンスを新しい Adobe Analytics for Streaming Media データタイプに移行する方法を説明します
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 3056a384535b3f5f2a9bc2d950bd5ee3410ec0a5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 47%

---

# Adobe Experience PlatformとCustomer Journey Analyticsの Media Analytics パラメーターマッピング

このドキュメントでは、Adobe Experience PlatformとCustomer Journey Analytics内で使用されるすべての Media Analytics パラメーターの包括的なリストを提供します。 これは、[Analytics Source Connector](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics) または [Analytics Adobe Analytics Source Connector for Classifications](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications) を介して Platform から読み込まれたデータの統合をサポートし、各パラメーターを対応する XDM フィールドパスにマッピングすることを目的としています。

## Media Analytics 予約変数

すべての Media Analytics 予約変数について、2025 年 5 月まで（および 2025 年 5 月を含む）にAdobe AnalyticsからAEPに取り込まれたデータは、以下の表で指摘されている「現在の XDM フィールドパス」で確認できます。

Media Analytics チームと ADC チームは現在、「レポート XDM フィールドパス」への完全移行に向けて取り組んでいるので、この移行が完了し、「レポート XDM フィールドパス」が使用できるようになると、公式コミュニケーションが共有されます。

## ストリーミングメディアパラメーター

| フィールド名 | 現在の XDM フィールドパス （非推奨） | レポート XDM フィールドのパス | データタイプ | 派生フィールド | メモ |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| ストリームタイプ | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | ディメンション | ストリームタイプ |                                                                       |
| コンテンツ ID | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | ディメンション | コンテンツ ID |                                                                       |
| コンテンツの長さ | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | ディメンション | コンテンツの長さ |                                                                       |
| コンテンツタイプ | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | ディメンション | コンテンツタイプ |                                                                       |
| メディアセッション ID | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | ディメンション | メディアセッション ID |                                                                       |
| コンテンツプレイヤー名 | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | ディメンション | コンテンツプレイヤー名 |                                                                       |
| コンテンツチャネル | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | ディメンション | コンテンツチャネル |                                                                       |
| コンテンツセグメント | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | ディメンション | コンテンツセグメント |                                                                       |
| コンテンツ名 | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | ディメンション | コンテンツ名 |                                                                       |
| ビデオパス | *AEP/CJAでは使用されません* |                                                   |           |                   | Adobe Analytics固有のプロパティ |
| 番組 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | ディメンション | 番組 |                                                                       |
| シーズン | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | ディメンション | シーズン |                                                                       |
| エピソード | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | ディメンション | エピソード |                                                                       |
| ジャンル | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | ディメンション | サポートなし | MediaReporting フィールドの使用 |
| ネットワーク | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | ディメンション | ネットワーク |                                                                       |
| 番組タイプ | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | ディメンション | 番組タイプ |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | ディメンション | MVPD |                                                                       |
| 認証済み | サポートなし | mediaReporting.sessionDetails.authorized | ディメンション | 認証済み |                                                                       |
| 日パート | サポートなし | mediaReporting.sessionDetails.dayPart | ディメンション | 日パート |                                                                       |
| メディアフィードのタイプ | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | ディメンション | メディアフィードのタイプ |                                                                       |
| 作者名 | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | ディメンション | 作者名 |                                                                       |
| アルバム | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | ディメンション | アルバム |                                                                       |
| ラベル | サポートなし | mediaReporting.sessionDetails.label | ディメンション | ラベル |                                                                       |
| 作成者 | サポートなし | mediaReporting.sessionDetails.author | ディメンション | 作成者 |                                                                       |
| ステーション | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | ディメンション | ステーション |                                                                       |
| 発行者 | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | ディメンション | 発行者 |                                                                       |
| メディア開始 | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | 指標 | メディア開始 |                                                                       |
| コンテンツ開始 | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | 指標 | コンテンツ開始 |                                                                       |
| コンテンツ完了 | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | 指標 | コンテンツ完了 |                                                                       |
| コンテンツ視聴時間 | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | 指標 | コンテンツ視聴時間 |                                                                       |
| メディア視聴時間 | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | 指標 | メディア視聴時間 |                                                                       |
| ユニーク再生時間 | サポートなし | mediaReporting.sessionDetails.uniqueTimePlayed | 指標 | ユニーク再生時間 |                                                                       |
| 10%進捗状況マーカー | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | 指標 | 10%進捗状況マーカー |                                                                       |
| 25%進捗状況マーカー | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | 指標 | 25%進捗状況マーカー |                                                                       |
| 50％進捗状況マーカー | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | 指標 | 50％進捗状況マーカー |                                                                       |
| 75%進捗状況マーカー | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | 指標 | 75%進捗状況マーカー |                                                                       |
| 95%進捗状況マーカー | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | 指標 | 95%進捗状況マーカー |                                                                       |
| 分平均オーディエンス | サポートなし | mediaReporting.sessionDetails.averageMinuteAudience | 指標 | 分平均オーディエンス |                                                                  |
| 前回の呼び出しからの経過時間（秒） | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | 指標 | 前回の呼び出しからの経過時間（秒） |                                                              |
| 一時停止の影響を受けたストリーム | サポートなし | mediaReporting.sessionDetails.hasPauseImpactedStreams | 指標 | 一時停止の影響を受けたストリーム | 他のイベントからこの値を計算することで、mediaTimed をカバーします |
| 一時停止イベント | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | 指標 | 一時停止イベント |                                                                       |
| 一時停止時間合計 | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | 指標 | 一時停止時間合計 |                                                                       |
| コンテンツ再開 | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | 指標 | コンテンツ再開 |                                                                       |
| コンテンツセグメント視聴回数 | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | 指標 | コンテンツセグメント視聴回数 |                                                                     |

{style="table-layout:auto"}

## プレーヤーステートパラメーターの更新

| フィールド名 | 現在の XDM フィールドパス （非推奨） | レポート XDM フィールドのパス | データタイプ | 派生フィールド | メモ |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| プレーヤーの状態の影響を受けるストリーム | サポートなし | mediaReporting.states.isSet | 指標 | サポートなし | mediaReporting フィールドの使用 |
| プレーヤーの状態のカウント | サポートなし | mediaReporting.states.count | 指標 | サポートなし | mediaReporting フィールドの使用 |
| プレイヤーの状態の合計期間 | サポートなし | mediaReporting.states.time | 指標 | サポートなし | mediaReporting フィールドの使用 |
| プレイヤーの州名 | サポートなし | mediaReporting.states.name | ディメンション | サポートなし | mediaReporting フィールドの使用 |

{style="table-layout:auto"}

## チャプターパラメーター 

| フィールド名 | 現在の XDM フィールドパス （非推奨） | レポート XDM フィールドのパス | データタイプ | 派生フィールド | メモ |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| チャプター | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | ディメンション | チャプター |           |
| チャプター開始 | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | 指標 | チャプター開始 |           |
| チャプター完了 | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | 指標 | チャプター完了 |          |
| チャプター閲覧時間 | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | 指標 | チャプター閲覧時間 |        |

{style="table-layout:auto"}

## 広告パラメーター 

| フィールド名 | 現在の XDM フィールドパス （非推奨） | レポート XDM フィールドのパス | データタイプ | 派生フィールド | メモ |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 広告 ID | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | ディメンション | 広告 ID |           |
| ポッド位置の広告 | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | ディメンション | ポッド位置の広告 |     |
| 広告の長さ | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | 指標 | 広告の長さ |           |
| 広告プレーヤー名 | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | ディメンション | 広告プレーヤー名 |           |
| 広告ブレーク ID | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | ディメンション | 広告ブレーク ID |           |
| 広告名 | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | ディメンション | 広告名 |           |
| 広告主 | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | ディメンション | 広告主 |           |
| キャンペーン ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | ディメンション | キャンペーン ID |           |
| 広告開始 | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | 指標 | 広告開始 |           |
| 広告完了 | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | 指標 | 広告完了 |           |
| 広告滞在時間 | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | 指標 | 広告滞在時間 |           |

{style="table-layout:auto"}

## 品質パラメーター 

| フィールド名 | 現在の XDM フィールドパス （非推奨） | レポート XDM フィールドのパス | データタイプ | 派生フィールド | メモ |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 平均ビットレート | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Both | 平均ビットレート |           |
| 開始時間 | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Both | 開始時間 |           |
| ドロップフレーム | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Both | ドロップフレーム |           |
| バッファーイベント | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Both | バッファーイベント |           |
| 合計バッファー時間 | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Both | 合計バッファー時間 |     |
| ビットレート変更 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Both | ビットレート変更 |         |
| エラー／エラーイベント | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Both | エラー／エラーイベント |  |
| プレーヤー SDK のエラー ID | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | ディメンション | サポートなし | mediaReporting フィールドの使用 |
| 外部エラー ID | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | ディメンション | サポートなし | mediaReporting フィールドの使用 |
| 開始前にドロップ | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | 指標 | 開始前にドロップ |     |
| バッファーの影響を受けたストリーム | サポートなし | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | 指標 | バッファーの影響を受けたストリーム | 他のイベントから計算 |
| ビットレート変更の影響を受けたストリーム | サポートなし | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | 指標 | ビットレート変更の影響を受けたストリーム | 他のイベントから計算 |
| エラーの影響を受けたストリーム | サポートなし | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | 指標 | エラーの影響を受けたストリーム | 他のイベントから計算 |
| ドロップフレームの影響を受けたストリーム | サポートなし | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | 指標 | ドロップフレームの影響を受けたストリーム | 他のイベントから計算 |

{style="table-layout:auto"}

## Media Analytics の分類

Media Analytics の分類は、ACDC と呼ばれる別のフローを介してAEPに取り込まれます。 次の表に示す各分類グループは、AEP内の一意のデータセットに対応します。 CJAでは、Media Analytics イベントデータセットと各分類データセット間の接続を確立する必要があります。

### Customer Journey Analyticsのデータセットの接続

Customer Journey Analyticsで接続を設定するには：

- 「**接続**」タブに移動し、「**新しい接続を作成**」を選択します。
- 接続インターフェイスで、「**データセットを追加**」を選択し、（ADC 経由でメディアデータをインポートするために使用される） Media Analytics イベントデータセットと、4 つの関連する分類データセットを探します。

### 設定の詳細

各ルックアップデータセット（分類データセット）について、次のように設定します。

- **ビデオデータセット**:
   - キー：`_sandbox.key`
   - 一致するキー：`Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - データ ソースの種類：`Web Data`

- **videoad データセット**:
   - キー：`_sandbox.key`
   - 一致するキー：`Ad ID (advertising.adAssetReference._id)`
   - データ ソースの種類：`Web Data`

- **videoadpod データセット**:
   - キー：`_sandbox.key`
   - 一致するキー：`Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - データ ソースの種類：`Web Data`

- **videochapter データセット**:
   - キー：`_sandbox.key`
   - 一致するキー：`Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - データ ソースの種類：`Web Data`

### レポートに関する考慮事項

レポート中に分類データセットを操作する場合は、標準の Media Analytics XDM フィールドではなく、分類固有のフィールドパス（`ACDC XDM Path`）を参照していることを確認してください。

## 分類テーブル

| 分類名（グループ） | フィールド名 | ACDC XDM パス |
|------------|----------|-------------|
| video | キー/アセット ID | `<_sandbox>.key` |
| video | ビデオの長さ | `<_sandbox>.video_length` |
| video | ビデオ名 | `<_sandbox>.video_name` |
| video | アセット ID | `<_sandbox>.asset_id` |
| video | 初回放送日 | `<_sandbox>.first_air_date` |
| video | 初回デジタル日 | `<_sandbox>.first_digital_date` |
| video | コンテンツ評価 | `<_sandbox>.content_rating` |
| video | 作成者 | `<_sandbox>.originator` |
| videoad | キー/広告 ID | `<_sandbox>.key` |
| videoad | 広告の長さ | `<_sandbox>.ad_length` |
| videoad | 広告名 | `<_sandbox>.ad_name` |
| videoad | クリエイティブ ID | `<_sandbox>.creative_id` |
| videoadpod | キー/広告ポッド ID | `<_sandbox>.key` |
| videoadpod | ポッド位置 | `<_sandbox>.pod_position` |
| videoadpod | ポッド名 | `<_sandbox>.pod_name` |
| videochapter | キー/チャプター | `<_sandbox>.key` |
| videochapter | チャプターの長さ | `<_sandbox>.chapter_length` |
| videochapter | チャプターオフセット | `<_sandbox>.chapter_offset` |
| videochapter | チャプター位置 | `<_sandbox>.chapter_position` |
| videochapter | チャプター名 | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Media Analytics カスタム変数

Adobe Analyticsでは、各レポートスイート内で定義される実装ルールに応じて、カスタム変数が様々なイベントや eVar に割り当てられます。 その結果、これらのカスタム変数がAdobe Experience Platform（AEP）に読み込まれると、異なる XDM パスにマッピングされます。

- イベントは、次のパスに保存されます。

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVar は、次のパスに保存されます。

  `_experience.analytics.customDimensions.eVars.eVar<number>`

どちらの場合も、`<number>` は元のAdobe Analytics レポートスイート設定で使用された特定のイベントまたはeVar番号に対応しています。

### カスタム変数

| フィールド名 | XDM パス | データタイプ |
|-------------|-------------|-----------|
| メディアダウンロード済みフラグ | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| SDK バージョン | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| VHL バージョン | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| ストリーム形式 | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| 初回放送日 | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| 初回デジタル日 | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| フェデレーテッドデータ | `_experience.analytics.customDimensions.eVars.eVar<number>` と `_experience.analytics.event<x>to<y>.event<number>.value` | Both |
| 推定ストリーム | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| 広告数 | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| チャプター数 | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| クリエイティブ ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| サイト ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| クリエイティブ URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| プレースメント ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | ディメンション |
| フレーム／秒 | `_experience.analytics.customDimensions.eVars.eVar<number>` と `_experience.analytics.event<x>to<y>.event<number>.value` | Both |
| メディア SDK のエラー ID | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| 停止の影響を受けたストリーム | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| 停止イベント | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |
| 合計停止時間 | `_experience.analytics.event<x>to<y>.event<number>.value` | 指標 |

{style="table-layout:auto"}






