---
title: ストリーミングメディアサービスのリリースノート
description: ストリーミングメディアサービスのリリースノートを参照してください。
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 528a82a4299370c2ef5a366b1f3fab9fd21b164f
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 69%

---

# ストリーミングメディアサービスのリリースノート（2025年10月）

**最終更新日**：2025年10月7日（PT）

## 関連リソース

新機能、修正点、および管理者向けの重要な情報について詳しくは、次のリソースを参照してください。

* [Adobe Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=ja)
* [Customer Journey Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=ja)
* [Adobe Experience Cloud 製品](https://business.adobe.com/jp/products/adobe-experience-cloud-products.html)の最新のリリース更新

* [Adobe Analytics チュートリアル](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=ja)

## *最新のリリースノート*

## Adobe ストリーミングメディアサービスの新機能と更新機能 {#cja-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| **ストリーミングメディア：スケジュールデータのサポート** | 過去のライブストリーミングメディアコンテンツのスケジュールデータをアップロードして、閲覧者数をより簡単かつ正確に追跡できるようになりました。<p>以下は、スケジュールデータのアップロードでサポートされるライブコンテンツの例です。</p><ul><li>FAST（無料広告サポート TV）プラットフォーム</li><li>ローカルストリーム</li><li>ライブスポーツ</li></ul><p>スケジュールデータをアップロードすると、アップロードファイルで指定した時間帯に放送された個々の番組の閲覧者数データを追跡できます。 特定のトピックやプログラムセグメントの閲覧者数データを収集することもできます。</p><p>これらの機能は、ストリーミングメディアコレクションの実装方法に関係なく使用できます。</p><p>以前は、ライブコンテンツを分析する際に、特定のセッションを特定のプログラムに正確に紐付けることが難しく、特定のセッションを個々のトピックやプログラムセグメントに紐付けることはできませんでした。</p><p>詳しくは、[スケジュールデータをアップロードしてライブコンテンツを追跡する](https://experienceleague.adobe.com/ja/docs/media-analytics/using/media-use-cases/track-schedule-data)を参照してください。</p> | ロールアウト開始：2025年10月29日（PT）<p>一般公開：2026年上半期</p><p>（当初は2025年10月29日に一般公開予定）</p> |
| ストリーミングメディアデータをAdobe Experience Platformに収集するためのXDM フィールドを更新しました | ストリーミングメディアデータを Adobe Experience Platform に収集する際は、ストリーミングメディアパラメーターに関するドキュメントの「XDM フィールドパス」の見出しの下に表示されている XDM フィールドパスは使用しないでください。 2025年5月9日（PT）より前に Analytics ソースコネクタを実装し、ストリーミングメディアデータを Platform に収集しているお客様は、ストリーミングメディアパラメーターに関するドキュメントの「XDM フィールドパスのレポート」の見出しの下に示されているように、既存の設定を mediaReporting フィールドパスに移行する必要があります。<p> これらのフィールドパスは、[オーディオおよびビデオパラメーター](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/audio-video-parameters)、[広告パラメーター](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/ad-parameters)、[チャプターパラメーター](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/chapter-parameters)、[プレーヤー状態パラメーター](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/player-state-parameters)および[品質パラメーター](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/quality-parameters)のページに表示されますが、「廃止」としてマークされています。 （2025年5月9日（PT）以降に Analytics ソースコネクタを実装し、既に mediaReporting XDM パスのみを使用しているお客様は、アクションは必要ありません。）</p><p>廃止された XDM フィールドパスでのデータ取り込みは、2025年10月末まで継続されます。 その後、廃止されたフィールドは完全に廃止され、Adobe Experience Platform スキーマ UI に表示されなくなります。データは mediaReporting フィールドを使用してのみ送信されるようになります。</p><p>詳しくは、[更新された XDM ストリーミングメディアフィールドへの Analytics ソースコネクターの実装の移行](/help/use-cases/xdm-updates/updated-xdm-fields.md)を参照してください。</p><p>移行のサポートについては、Adobe Consulting サービスまたはアカウントチームにお問い合わせください。 </p> | 2025年10月 |
| Web SDKを使用して、Adobe Experience Platform Edge Networkにweb データを送信する | [Adobe Experience Platform Web SDKを使用して、Adobe Experience Platform Edge Networkにストリーミングメディア web データを送信できるようになりました](/help/implementation/edge/edge-web-sdk.md)。これにより、よりパーソナライズされたキャンペーンを構築し、よりパーソナライズされたコンテンツを提供できるようになりました。その結果、レポート用のトラッキングデータが増加しました。<p>この機能強化により、Customer Journey Analytics、RT-CDP、AJO、イベント転送など、すべてのプラットフォームソリューションをまたいだ web 実装向けの、統一された収集方法が提供されます。 以前は、ストリーミングメディア web データを Edge Network に送信する唯一の方法は、Media Edge API を使用することでした。 | 2024年5月29日（PT） |
| Roku データをAdobe Experience Platform Edgeに送信する | 現在、[Experience Platform Edgeを使用してCustomer Journey Analytics Streaming Media Collectionをインストールする場合](/help/implementation/edge/implementation-edge.md)、Adobe Experience Platform Roku SDKを使用してAdobe Experience Platformにストリーミングメディアデータを送信できます。 | 2024年4月12日（PT） |
| Media Collection: Experience Edgeとの統合（APIおよびモバイルSDK） | Adobe Experience Edge APIとモバイルSDKを使用してCustomer Journey Analytics Streaming Media Collectionを実装できるようになりました。これにより、よりパーソナライズされたキャンペーンを構築し、よりパーソナライズされたコンテンツを提供して、レポート用のトラッキングデータを増やすことができます。<p>この機能強化により、Customer Journey Analytics レポート、RT-CDP、AJO、イベント転送など、すべてのソリューションで統一された収集方法が提供されます。  [詳細情報](/help/implementation/edge/implementation-edge.md) | 2023年5月12日（PT） |
| メディア同時ビューアパネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。 Adobe insightを利用して、コンテンツの質と視聴者のエンゲージメントを把握し、コンテンツの量と規模に関するトラブルシューティングや計画を立案できます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=ja) | 2022年8月9日（PT） |
| メディア再生滞在時間パネル | メディア再生滞在時間は、ビューアエンゲージメントに関する貴重なインサイトを提供し、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。 特定の時点でのメディアストリームの視聴時間を確認できます。 再生時間は、新しい5分、15分、30分の精度など、様々な精度で分割できます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=ja) | 2022年8月9日（PT） |
| モバイルスコアカードで注釈を共有 | ワークスペースで作成された注釈をモバイルスコアカードに表示できます。 これにより、Analytics ダッシュボードのモバイルアプリで表示できる、組織やキャンペーンに関するコンテキストデータのニュアンスとインサイトを、モバイルスコアカードプロジェクト内で直接共有できます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=ja) | 2022年6月15日（PT） |
| Customer Journey Analytics の Report Builder の更新 | スケジュール設定やデータブロックマネージャーなどの機能が含まれています。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=ja) | 2022年5月18日（PT） |
| ワークスペースの注釈 | Workspaceの注釈を使用すると、コンテクストに即したデータのニュアンスとインサイトを効果的に組織に伝えることができます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=ja) | 2022年3月23日（PT）から順次展開を開始 |
| モバイルスコアカードプロジェクトのプレビューモード | Analytics ダッシュボードアプリにおけるモバイルスコアカードの表示のプレビューを、スコアカードビルダーから直接起動します。 プレビューモードを使用すると、アプリ内と同じ方法でフィルターやグラフを操作でき、スコアカードを保存および共有する前にエクスペリエンスをプレビューできます。 また、プレビューモードでデバイスピッカーを使用して、さまざまなデバイスでスコアカードがどのように表示されるかを確認することもできます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=ja#preview) | 2022年2月16日 |


## Adobe ストリーミングメディアサービスの新機能と更新機能 {#sm-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| 複数のプレーヤーの状態トラッキング | メディア収集APIを使用して、複数のプレーヤーの状態トラッキングを実装します。[詳細情報](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=ja) | 2022年9月 |
| XDM フィールドの名前を変更しました | 一貫性を保つために次の XDM フィールド名を変更しました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーの状態パラメーター<br>*品質パラメーター | 2022年9月 |
| Device Co-op リファレンス | Adobe Experience Cloud Device Co-op および Experience Cloud ID サービスの要件へのリファレンスを削除しました。 | 2022年8月 |
| コレクションおよびレポートのフィールド名と XDM パスを更新しました | 次のパラメーターが更新されました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーステートパラメーター<br>*品質パラメーター | 2022年8月 |
| 分平均オーディエンス | Adobe Media Analyticsの顧客は、「毎分平均オーディエンス数」パネルを使用して、平均コンテンツ消費量をより詳細に把握できます。<br>分平均オーディエンスを使用すると、任意の長さやジャンルのプログラミングを比較できます。 さらに、お客様はデジタル分平均オーディエンスを、線形 TV 分平均指標と比較したり、この指標に追加したりできます。 このパネルでは、カスタム期間の平均オーディエンスをより柔軟に測定できるほか、期間の分類が更新された場合にも測定できます。  [詳細情報](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=ja) | 2022年3月16日（PT） |
| メディア再生滞在時間パネル | メディア再生滞在時間パネルを使用して、選択した精度で日中に視聴した時間で視聴者を把握する方法について説明します。<br>[メディア再生滞在時間パネル （チュートリアル） ](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=ja) | 2022年1月 |


## *以前のリリースノート*

| 機能 | 説明 | ターゲット日または更新日 |
| ----------- | ---------- | -------------- |
| メディア再生滞在時間 | アドビのストリーミングメディア再生滞在時間は、ビューアのエンゲージメントに関する貴重なインサイトを提供します。これにより、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。 特定の時点でのメディアストリームの視聴時間を確認できます。 再生時間は、新しい5分、15分、30分など、様々な精度で分割できます。[詳細情報…](/help/reporting/workspace/media-playback-time-spent.md) | 2021年9月 |
| Analytics Workspace のメディア同時閲覧者パネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。 Adobe insightを利用して、コンテンツの質と視聴者のエンゲージメントを把握し、コンテンツの量と規模に関するトラブルシューティングや計画を立案できます。[詳細…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspaceのメディア同時視聴者数パネル （チュートリアル） ](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=ja#analysis-workspace) | 2020年9月<br><br><br> 2021年1月 |
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
