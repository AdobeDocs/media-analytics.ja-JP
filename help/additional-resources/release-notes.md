---
title: ストリーミングメディアサービスのリリースノート
description: ストリーミングメディアサービスのリリースノートを参照してください。
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: f73667dc-d296-4875-8975-ac3fdc3adc42id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: ac8a38fa-dec3-4581-8f64-178fde9f64e8id: c77ba355-6681-41fe-b719-563d3f507fdbid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 1516
ht-degree: 79%

---

# ストリーミングメディアサービスのリリースノート（2025年10月）

**最終更新日**：2025年10月7日（PT）

## 関連リソース

新機能、修正点、および管理者向けの重要な情報について詳しくは、次のリソースを参照してください。

* [Adobe Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=ja)
* [Customer Journey Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=ja)
* [Adobe CX Enterprise](https://business.adobe.com/jp/products/adobe-experience-cloud-products.html)の最新のリリースアップデート

* [Adobe Analytics チュートリアル](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=ja)

## *最新のリリースノート*

## Adobe ストリーミングメディアサービスの新機能と更新機能 {#cja-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| **ストリーミングメディア：スケジュールデータのサポート** | 過去のライブストリーミングメディアコンテンツのスケジュールデータをアップロードして、閲覧者数をより簡単かつ正確に追跡できるようになりました。<p>以下は、スケジュールデータのアップロードでサポートされるライブコンテンツの例です。</p><ul><li>FAST（無料広告サポート TV）プラットフォーム</li><li>ローカルストリーム</li><li>ライブスポーツ</li></ul><p>スケジュールデータをアップロードすると、アップロードファイルで指定した時間帯に放送された個々の番組の閲覧者数データを追跡できます。 特定のトピックやプログラムセグメントの閲覧者数データを収集することもできます。</p><p>これらの機能は、ストリーミングメディアコレクションの実装方法に関係なく使用できます。</p><p>以前は、ライブコンテンツを分析する際に、特定のセッションを特定のプログラムに正確に紐付けることが難しく、特定のセッションを個々のトピックやプログラムセグメントに紐付けることはできませんでした。</p><p>詳しくは、[スケジュールデータをアップロードしてライブコンテンツを追跡する](/help/use-cases/track-schedule-data.md)を参照してください。</p> | ロールアウト開始：2025年10月29日（PT）<p>一般公開：2026年上半期</p><p>（当初は2025年10月29日に一般公開予定）</p> |
| ストリーミングメディアデータをAdobe Experience Platformに収集するためのXDM フィールドを更新しました | ストリーミングメディアデータを Adobe Experience Platform に収集する際は、ストリーミングメディアパラメーターに関するドキュメントの「XDM フィールドパス」の見出しの下に表示されている XDM フィールドパスは使用しないでください。 2025年5月9日（PT）より前に Analytics ソースコネクタを実装し、ストリーミングメディアデータを Platform に収集しているお客様は、ストリーミングメディアパラメーターに関するドキュメントの「XDM フィールドパスのレポート」の見出しの下に示されているように、既存の設定を mediaReporting フィールドパスに移行する必要があります。<p> これらのフィールドパスは、[ ストリーミングメディアサービスの概要](../media-overview.md)からリンクされたストリーミングメディア変数ページに記載されており、「非推奨」とマークされています。 （2025年5月9日（PT）以降に Analytics ソースコネクタを実装し、既に mediaReporting XDM パスのみを使用しているお客様は、アクションは必要ありません。）</p><p>廃止された XDM フィールドパスでのデータ取り込みは、2025年10月末まで継続されます。 その後、廃止されたフィールドは完全に廃止され、Adobe Experience Platform スキーマ UI に表示されなくなります。データは mediaReporting フィールドを使用してのみ送信されるようになります。</p><p>詳しくは、[Adobe Experience PlatformとCustomer Journey AnalyticsのMedia Analytics パラメーターのマッピングを参照してください](/help/implementation/parameters-mapping.md)。</p><p>移行のサポートについては、Adobe Consulting サービスまたはアカウントチームにお問い合わせください。 </p> | 2025年10月 |
| Web SDKを使用して、Adobe Experience Platform Edge Networkにweb データを送信する | [Adobe Experience Platform Web SDKを使用して、Adobe Experience Platform Edge Networkにストリーミングメディア web データを送信できるようになりました](/help/implementation/edge/edge-web-sdk.md)。これにより、よりパーソナライズされたキャンペーンを構築し、よりパーソナライズされたコンテンツを提供できるようになりました。その結果、レポート用のトラッキングデータが増加しました。<p>この機能強化により、Customer Journey Analytics、RT-CDP、AJO、イベント転送など、すべてのプラットフォームソリューションをまたいだ web 実装向けの、統一された収集方法が提供されます。 以前は、ストリーミングメディア web データを Edge Network に送信する唯一の方法は、Media Edge API を使用することでした。 | 2024年5月29日（PT） |
| Roku データをAdobe Experience Platform Edgeに送信する | 現在、[Experience Platform Edgeを使用してCustomer Journey Analytics Streaming Media Collectionをインストールする場合](/help/implementation/edge/implementation-edge.md)、Adobe Experience Platform Roku SDKを使用してAdobe Experience Platformにストリーミングメディアデータを送信できます。 | 2024年4月12日（PT） |
| Media Collection: Experience Edgeとの統合（APIおよびモバイルSDK） | Adobe Experience Edge APIとモバイルSDKを使用してCustomer Journey Analytics Streaming Media Collectionを実装できるようになりました。これにより、よりパーソナライズされたキャンペーンを構築し、よりパーソナライズされたコンテンツを提供して、レポート用のトラッキングデータを増やすことができます。<p>この機能強化により、Customer Journey Analytics レポート、RT-CDP、AJO、イベント転送など、すべてのソリューションで統一された収集方法が提供されます。  [詳細情報](/help/implementation/edge/implementation-edge.md) | 2023年5月12日（PT） |
| メディア同時ビューアパネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。 コンテンツの質と閲覧者のエンゲージメントに関する貴重なインサイトを取得でき、ボリュームやスケールのトラブルシューティングや計画に役立ちます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=ja) | 2022年8月9日（PT） |
| メディア再生滞在時間パネル | メディア再生滞在時間は、ビューアエンゲージメントに関する貴重なインサイトを提供し、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。 特定の時点でのメディアストリームの視聴時間を確認できます。 再生時間は、新たな 5 分、15 分、30 分の時間粒度を含む、様々な粒度で分割できます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=ja) | 2022年8月9日（PT） |
| モバイルスコアカードで注釈を共有 | ワークスペースで作成された注釈をモバイルスコアカードに表示できます。 これにより、組織とキャンペーンに関するコンテキストデータのニュアンスやインサイトを、モバイルスコアカードプロジェクト内で直接共有でき、Analytics ダッシュボードモバイルアプリで表示できます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=ja) | 2022年6月15日（PT） |
| Customer Journey Analytics の Report Builder の更新 | スケジュールおよびデータブロックマネージャーなどの機能が含まれます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=ja) | 2022年5月18日（PT） |
| ワークスペースの注釈 | Analysis Workspace の注釈を使用すると、コンテキストデータのニュアンスとインサイトを組織に効果的に伝えることができます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=ja) | 2022年3月23日（PT）から順次展開を開始 |
| モバイルスコアカードプロジェクトのプレビューモード | Analytics ダッシュボードアプリにおけるモバイルスコアカードの表示のプレビューを、スコアカードビルダーから直接起動します。 プレビューモードを使用すると、アプリ内と同じ方法でフィルターやグラフを操作でき、スコアカードを保存および共有する前にエクスペリエンスをプレビューできます。 また、デバイスピッカーをプレビューモードで使用して、様々なデバイスでのスコアカードの表示を確認することもできます。 [詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=ja#preview) | 2022年2月16日 |


## Adobe ストリーミングメディアサービスの新機能と更新機能 {#sm-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| 複数のプレーヤーの状態トラッキング | Media Collection API を使用して、複数のプレーヤーの状態トラッキングを実装します。 [詳細情報](/help/implementation/events/player-state/overview.md) | 2022年9月 |
| XDM フィールドの名前を変更しました | 一貫性を保つために次の XDM フィールド名を変更しました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーの状態パラメーター<br>*品質パラメーター | 2022年9月 |
| Device Co-op リファレンス | デバイス Co-opとID サービス要件への参照を削除しました。 | 2022年8月 |
| コレクションおよびレポートのフィールド名と XDM パスを更新しました | 次のパラメーターが更新されました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーステートパラメーター<br>*品質パラメーター | 2022年8月 |
| 分平均オーディエンス | Media Analytics のお客様は、分平均オーディエンスパネルを使用すると、コンテンツの平均消費量をより正確に把握できます。 <br>分平均オーディエンスを使用すると、あらゆる長さやジャンルのプログラミングを比較できます。 さらに、お客様はデジタル分平均オーディエンスを、線形 TV 分平均指標と比較したり、この指標に追加したりできます。 このパネルでは、カスタム期間の平均オーディエンスをより柔軟に測定できるほか、期間の分類が更新された場合にも測定できます。  [詳細情報](/help/reporting/workspace/average-minute-audience.md) | 2022年3月16日（PT） |
| メディア再生滞在時間パネル | メディアユーザーがメディア再生時間パネルを使用して、1 日の閲覧時間に基づいた視聴者数を、指定された精度で把握する方法を説明します。 <br>[メディア再生滞在時間パネル（チュートリアル）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=ja) | 2022年1月 |


## *以前のリリースノート*

| 機能 | 説明 | ターゲット日または更新日 |
| ----------- | ---------- | -------------- |
| メディア再生滞在時間 | アドビのストリーミングメディア再生滞在時間は、ビューアのエンゲージメントに関する貴重なインサイトを提供します。これにより、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。 特定の時点でのメディアストリームの視聴時間を確認できます。 再生時間は、様々な粒度（新たな 5 分、15 分、30 分の時間粒度を含む）で分割できます。 [詳細情報...](/help/reporting/workspace/media-playback-time-spent.md) | 2021年9月 |
| Analytics Workspace のメディア同時閲覧者パネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。 コンテンツの質と閲覧者のエンゲージメントに関する貴重なインサイトを取得でき、ボリュームやスケールのトラブルシューティングや計画に役立ちます。 [詳細情報…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspace のメディア同時閲覧者パネル（チュートリアル）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=ja#analysis-workspace) | 2020年9月<br><br><br> 2021年1月 |
| サポートされるデバイスとプラットフォーム | AEP SDK を含むメディア Launch 拡張機能で、以下の OTT デバイスがサポートされるようになりました。 <div><ul><li>Apple TV（tvOS）</li><li>Fire TV（Fire OS）</li><li>Android TV</li></ul></div> | 2020年6月 |


<!--
## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | 
-->
