---
title: Adobe Experience PlatformとCustomer Journey AnalyticsのMedia Analytics パラメーターマッピング
description: Analytics Source コネクタおよびCustomer Journey Analyticsで使用されるMedia Analytics パラメーターのXDM フィールドパスマッピング。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1331
ht-degree: 20%

---

# Adobe Experience PlatformとCustomer Journey AnalyticsのMedia Analytics パラメーターマッピング

このドキュメントでは、Adobe Experience PlatformおよびCustomer Journey Analytics内で使用されるすべてのMedia Analytics パラメーターの包括的なリストを提供します。 これは、[Analytics Source コネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics)または[Analytics Source コネクタ for Classifications](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/classifications)を介してAdobe AnalyticsからPlatformに読み込まれたデータの統合をサポートし、各パラメーターを対応するXDM フィールドパスにマッピングすることを目的としています。

>[!NOTE]
>
>この参照は、[Analytics ソースコネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics)を使用して、Adobe AnalyticsからAdobe Experience Platformにストリーミングメディアデータを取り込み、Customer Journey Analytics レポートやその他のPlatform サービスで使用する組織に適用されます。 これらの変更は、データ収集、処理、レポートなど、Adobe Analytics as a スタンドアロンアプリケーションには影響しません。

## Media Analyticsの予約変数

2025年10月の時点で、Analytics ソースコネクタで使用される`media.mediaTimed` XDM フィールドパスは完全に非推奨となり、`mediaReporting`に置き換えられます。 2025年10月以降に取り込まれたデータには、`mediaReporting`個のフィールドのみが含まれます。 以前のデータは、従来のフィールドパスの下に残り、**従来のXDM フィールド**&#x200B;の下のテーブルに反映されます。

### キープアライブ通話動作

ストリーミングメディア用のAnalytics ソースコネクタを使用すると、Adobe Analyticsからのキープアライブ呼び出しがAdobe Experience Platformに取り込まれるようになりました。 これは、次のCustomer Journey Analytics レポートに影響を与える可能性があります。

* **セッション数**：キープアライブ呼び出しは、メディアとの直接インタラクションがなくても、アクティブユーザーセッションを維持するのに役立ちます。 これらの呼び出しは、メディア再生ごとに最後のイベントから20分ごとに生成されます。 最適なセッション追跡を確保するには、データビューで訪問の有効期限を30分に設定します。

* **イベント数**：キープアライブ呼び出しは、Customer Journey Analytics イベント指標にカウントされるようになりました。 除外するには、イベントタイプ `media.keepalive`のイベントを除外するフィルターを作成します。

## Streaming Media パラメーター

| フィールド名 | レガシーXDM フィールド | レポート XDM フィールドパス | データタイプ | 派生フィールド | メモ |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL  ストリームタイプ ]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | ディメンション | [[!UICONTROL  ストリームタイプ ]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL  コンテンツ ID]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | ディメンション | [[!UICONTROL  コンテンツ ID]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL  コンテンツの長さ]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | ディメンション | [[!UICONTROL  コンテンツの長さ]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL  コンテンツの種類]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | ディメンション | [[!UICONTROL  コンテンツの種類]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL  メディアセッション ID]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | ディメンション | [[!UICONTROL  メディアセッション ID]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL  コンテンツプレーヤー名]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | ディメンション | [[!UICONTROL  コンテンツプレーヤー名]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL  コンテンツチャネル ]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | ディメンション | [[!UICONTROL  コンテンツチャネル ]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL  コンテンツセグメント ]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | ディメンション | [[!UICONTROL  コンテンツセグメント ]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL  コンテンツ名]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | ディメンション | [[!UICONTROL  コンテンツ名]](/help/reporting/dimensions/content-name.md) | |
| ビデオパス | *AEP/CJAでは使用されていません* | | | | Adobe Analytics固有のプロパティ |
| [[!UICONTROL 表示]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | ディメンション | [[!UICONTROL 表示]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL  シーズン ]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | ディメンション | [[!UICONTROL  シーズン ]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL  エピソード ]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | ディメンション | [[!UICONTROL  エピソード ]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL  ジャンル ]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | ディメンション | サポートされていません | `mediaReporting` フィールドを使用 |
| [[!UICONTROL ネットワーク]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | ディメンション | [[!UICONTROL ネットワーク]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL  タイプを表示]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | ディメンション | [[!UICONTROL  タイプを表示]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | ディメンション | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL 認証済み]](/help/reporting/metrics/authorized.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | ディメンション | [[!UICONTROL 認証済み]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL 日パート ]](/help/reporting/dimensions/day-part.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | ディメンション | [[!UICONTROL 日パート ]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL  メディアフィードの種類]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | ディメンション | [[!UICONTROL  メディアフィードの種類]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL  アーティスト ]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | ディメンション | [[!UICONTROL  アーティスト ]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL  アルバム ]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | ディメンション | [[!UICONTROL  アルバム ]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL ラベル]](/help/reporting/dimensions/label.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.label` | ディメンション | [[!UICONTROL ラベル]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL 作成者]](/help/reporting/dimensions/author.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.author` | ディメンション | [[!UICONTROL 作成者]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL 駅]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | ディメンション | [[!UICONTROL 駅]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL 発行者]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | ディメンション | [[!UICONTROL 発行者]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL  メディア開始]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | 指標 | [[!UICONTROL  メディア開始]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL  コンテンツ開始]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | 指標 | [[!UICONTROL  コンテンツ開始]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL  コンテンツ完了]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | 指標 | [[!UICONTROL  コンテンツ完了]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL  コンテンツ滞在時間]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | 指標 | [[!UICONTROL  コンテンツ滞在時間]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL  メディア滞在時間]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | 指標 | [[!UICONTROL  メディア滞在時間]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL  ユニーク再生時間]](/help/reporting/metrics/unique-time-played.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | 指標 | [[!UICONTROL  ユニーク再生時間]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | 指標 | [[!UICONTROL 10%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | 指標 | [[!UICONTROL 25%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | 指標 | [[!UICONTROL 50%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | 指標 | [[!UICONTROL 75%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | 指標 | [[!UICONTROL 95%進行状況マーカー]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 分平均オーディエンス]](/help/reporting/metrics/average-minute-audience.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | 指標 | [[!UICONTROL 分平均オーディエンス]](/help/reporting/metrics/average-minute-audience.md) | |
| 前回の呼び出しからの経過時間（秒） | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | 指標 | 前回の呼び出しからの経過時間（秒） | |
| [[!UICONTROL 影響を受けるストリームを一時停止]](/help/reporting/metrics/paused-impacted-streams.md) | サポートなし | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | 指標 | [[!UICONTROL 影響を受けるストリームを一時停止]](/help/reporting/metrics/paused-impacted-streams.md) | mediaTimedでは、この値を他のイベントから計算します |
| [[!UICONTROL  イベントを一時停止]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | 指標 | [[!UICONTROL  イベントを一時停止]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL 合計一時停止の期間]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | 指標 | [[!UICONTROL 合計一時停止の期間]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL  コンテンツの再開]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | 指標 | [[!UICONTROL  コンテンツの再開]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL  コンテンツセグメントビュー]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | 指標 | [[!UICONTROL  コンテンツセグメントビュー]](/help/reporting/metrics/content-segment-views.md) | |

## プレーヤーの状態パラメーターの更新

| フィールド名 | レガシーXDM フィールド | レポート XDM フィールドパス | データタイプ | 派生フィールド | メモ |
| --- | --- | --- | --- | --- | --- |
| プレーヤーの状態の影響を受けるストリーム | サポートなし | `xdm.mediaReporting.`<br>`states.isSet` | 指標 | サポートされていません | `mediaReporting` フィールドを使用 |
| プレイヤーの状態カウント | サポートなし | `xdm.mediaReporting.`<br>`states.count` | 指標 | サポートされていません | `mediaReporting` フィールドを使用 |
| プレーヤーの状態の合計期間 | サポートなし | `xdm.mediaReporting.`<br>`states.time` | 指標 | サポートされていません | `mediaReporting` フィールドを使用 |
| プレーヤーの状態名 | サポートなし | `xdm.mediaReporting.`<br>`states.name` | ディメンション | サポートされていません | `mediaReporting` フィールドを使用 |

## チャプターパラメーター

| フィールド名 | レガシーXDM フィールド | レポート XDM フィールドパス | データタイプ | 派生フィールド | メモ |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 章]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | ディメンション | [[!UICONTROL 章]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL 章の開始]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | 指標 | [[!UICONTROL 章の開始]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL 章完了]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | 指標 | [[!UICONTROL 章完了]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL 章の滞在時間]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | 指標 | [[!UICONTROL 章の滞在時間]](/help/reporting/metrics/chapter-time-spent.md) | |

## 広告パラメーター

| フィールド名 | レガシーXDM フィールド | レポート XDM フィールドパス | データタイプ | 派生フィールド | メモ |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 広告ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | ディメンション | [[!UICONTROL 広告ID]](/help/reporting/dimensions/ad.md) | |
| ポッドの位置[[!UICONTROL 広告]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | ディメンション | ポッドの位置[[!UICONTROL 広告]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL 広告の長さ]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | 指標 | [[!UICONTROL 広告の長さ]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL 広告プレイヤー名]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | ディメンション | [[!UICONTROL 広告プレイヤー名]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL Ad Break ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | ディメンション | [[!UICONTROL Ad Break ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL 広告名]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | ディメンション | [[!UICONTROL 広告名]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL 広告主]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | ディメンション | [[!UICONTROL 広告主]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL キャンペーン ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | ディメンション | [[!UICONTROL キャンペーン ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | 指標 | [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL 広告完了]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | 指標 | [[!UICONTROL 広告完了]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL 広告滞在時間]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | 指標 | [[!UICONTROL 広告滞在時間]](/help/reporting/metrics/ad-time-spent.md) | |

## 品質パラメーター

| フィールド名 | レガシーXDM フィールド | レポート XDM フィールドパス | データタイプ | 派生フィールド | メモ |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 平均ビットレート ]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | 両方 | [[!UICONTROL 平均ビットレート ]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL 開始までの時間]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | 両方 | [[!UICONTROL 開始までの時間]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL 削除されたフレーム ]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | 両方 | [[!UICONTROL 削除されたフレーム ]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL  バッファーイベント ]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | 両方 | [[!UICONTROL  バッファーイベント ]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL 合計バッファー期間]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | 両方 | [[!UICONTROL 合計バッファー期間]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL  ビットレートの変更]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | 両方 | [[!UICONTROL  ビットレートの変更]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL  エラー/ エラーイベント ]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | 両方 | [[!UICONTROL  エラー/ エラーイベント ]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL Player SDK エラーID]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | ディメンション | サポートされていません | `mediaReporting` フィールドを使用 |
| [[!UICONTROL 外部エラーID]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | ディメンション | サポートされていません | `mediaReporting` フィールドを使用 |
| [[!UICONTROL 開始する前にドロップ ]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | 指標 | [[!UICONTROL 開始する前にドロップ ]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL 影響を受けるストリームのバッファー]](/help/reporting/metrics/buffer-impacted-streams.md) | サポートなし | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | 指標 | [[!UICONTROL 影響を受けるストリームのバッファー]](/help/reporting/metrics/buffer-impacted-streams.md) | 他のイベントから計算 |
| [[!UICONTROL  ビットレートの変更が影響を受けるストリーム ]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | サポートなし | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | 指標 | [[!UICONTROL  ビットレートの変更が影響を受けるストリーム ]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 他のイベントから計算 |
| [[!UICONTROL 影響を受けるストリームのエラー]](/help/reporting/metrics/error-impacted-streams.md) | サポートなし | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | 指標 | [[!UICONTROL 影響を受けるストリームのエラー]](/help/reporting/metrics/error-impacted-streams.md) | 他のイベントから計算 |
| [[!UICONTROL  ドロップされたフレームの影響を受けるストリーム ]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | サポートなし | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | 指標 | [[!UICONTROL  ドロップされたフレームの影響を受けるストリーム ]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 他のイベントから計算 |

## Media Analyticsの分類

Media Analyticsの分類は、ACDCと呼ばれる別のフローを介してAEPに取り込まれます。 次の表に示す各分類グループは、AEP内の一意のデータセットに対応します。 CJAでは、Media Analytics イベントデータセットと各分類データセットとの間の接続を確立する必要があります。

### Customer Journey Analyticsでのデータセットの接続

Customer Journey Analyticsで接続を設定するには：

* 「**接続**」タブに移動し、「**新しい接続を作成**」を選択します。
* 接続インターフェイスで、**データセットを追加**&#x200B;を選択し、4つの関連する分類データセットと共に、（ADC経由でメディアデータを読み込むために使用される） Media Analytics イベントデータセットを見つけます。

### 設定の詳細

ルックアップデータセット（分類データセット）ごとに、次のように設定します。

* **ビデオデータセット**:
   * キー：`_sandbox.key`
   * 一致するキー：`Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * データ ソースの種類：`Web Data`

* **ビデオデータセット**:
   * キー：`_sandbox.key`
   * 一致するキー：`Ad ID (advertising.adAssetReference._id)`
   * データ ソースの種類：`Web Data`

* **videoadpod データセット**:
   * キー：`_sandbox.key`
   * 一致するキー：`Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * データ ソースの種類：`Web Data`

* **ビデオチャプターデータセット**:
   * キー：`_sandbox.key`
   * 一致するキー：`Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * データ ソースの種類：`Web Data`

### レポートに関する検討事項

レポート中に分類データセットを使用する場合は、標準のMedia Analytics XDM フィールドではなく、分類固有のフィールドパス （`ACDC XDM Path`）を参照してください。

## 分類テーブル

| 分類名（グループ） | フィールド名 | ACDC XDM パス |
| --- | --- | --- |
| video | キー/アセット ID | `xdm.<_sandbox>.key` |
| video | ビデオの長さ | `xdm.<_sandbox>.video_length` |
| video | ビデオ名 | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL  アセット ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL 最初のエア日]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL 最初のデジタル日付]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL  コンテンツの評価]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL 発信元]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | キー/広告ID | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL 広告の長さ]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL 広告名]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | キー/広告ポッド ID | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL  ポッドの位置]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL  ポッド名]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | キー/章 | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL 章の長さ]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL 章のオフセット ]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL 章の位置]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL 章名]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Media Analytics カスタム変数

Adobe Analyticsでは、各レポートスイート内で定義された実装ルールに応じて、カスタム変数が異なるイベントまたはeVarに割り当てられます。 その結果、これらのカスタム変数がAdobe Experience Platform（AEP）に読み込まれると、異なるXDM パスにマッピングされます。

* イベントは、次のパスに保存されます。

  `_experience.analytics.event<x>to<y>.event<number>.value`

* eVarは、次のパスに格納されます。

  `_experience.analytics.customDimensions.eVars.eVar<number>`

いずれの場合も、`<number>`は、元のAdobe Analytics レポートスイート設定で使用されている特定のイベントまたはeVar番号に対応します。

### カスタム変数

| フィールド名 | XDM パス | データタイプ |
| --- | --- | --- |
| [[!UICONTROL  メディア ダウンロード フラグ ]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| SDK バージョン | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| Media Library バージョン | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL  ストリーム形式]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL 最初のエア日]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL 最初のデジタル日付]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL 連合データ ]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>および<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 両方 |
| [[!UICONTROL 推定ストリーム ]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL 広告数]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL 章数]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL  サイト ID]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL Creative URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| [[!UICONTROL  プレースメント ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | ディメンション |
| フレーム／秒 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>および<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 両方 |
| メディア SDK のエラー ID | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL 影響を受けるストリームを停止しています]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL  イベントの停止]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
| [[!UICONTROL 合計滞留期間]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 指標 |
