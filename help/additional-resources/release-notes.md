---
title: Streaming Media Collection リリースノート
description: Streaming Media Collection のリリースノートを表示します。
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 78%

---

# Streaming Media Collection リリースノート（2023 年 5 月）

**最終更新日**：2024年5月29日（PT）

## 関連リソース

新機能、修正点、および管理者向けの重要な情報について詳しくは、次のリソースを参照してください。

* [Adobe Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=ja)
* [Customer Journey Analytics リリースノート](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=ja)
* [Adobe Experience Cloud 製品](https://business.adobe.com/jp/products/adobe-experience-cloud-products.html)の最新のリリース更新

* [Adobe Analytics チュートリアル](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=ja)

## *最新のリリースノート*

## Adobeストリーミングメディアコレクションの新機能と更新された機能 {#cja-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| Web SDKを使用したAdobe Experience Platform Edge Networkへの web データの送信 | [Adobe Experience Platform Web SDKを使用して、ストリーミングメディアの web データをAdobe Experience Platform Edge Networkに送信 ](/help/implementation/edge/edge-web-sdk.md) できるようになりました。これにより、よりパーソナライズされたキャンペーンを作成し、よりパーソナライズされたコンテンツを提供して、レポートするトラッキングデータを増やすことができます。<p>この機能強化により、Customer Journey Analytics、RT-CDP、AJO、イベント転送など、すべてのプラットフォームソリューションをまたいだ web 実装向けの、統一された収集方法が提供されます。以前は、ストリーミングメディア web データを Edge Network に送信する唯一の方法は、Media Edge API を使用することでした。 | 2024年5月29日（PT） |
| Roku データのAdobe Experience Platform Edgeへの送信 | [Streaming Media Collection をExperience Platform Edgeと共にインストール ](/help/implementation/edge/implementation-edge.md) する際に、Adobe Experience Platform Roku SDKを使用してストリーミングメディアデータをAdobe Experience Platformに送信できるようになりました。 | 2024年4月12日（PT） |
| Media Collection: Experience Edgeとの統合（API およびモバイル SDK） | Experience Edge API とモバイル SDKを使用して、Adobeのストリーミングメディアコレクションを実装できるようになりました。これにより、よりパーソナライズされたキャンペーンを作成し、よりパーソナライズされたコンテンツを提供して、レポートするトラッキングデータを増やすことができます。<p>この機能強化により、Customer Journey Analyticsレポート、RT-CDP、AJO、イベント転送など、すべてのソリューションにわたって統一された収集手段が提供されます。  [詳細情報](/help/implementation/edge/implementation-edge.md) | 2023年5月12日（PT） |
| メディア同時ビューアパネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。コンテンツの質と閲覧者のエンゲージメントに関する貴重なインサイトを取得でき、ボリュームやスケールのトラブルシューティングや計画に役立ちます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=ja) | 2022年8月9日（PT） |
| メディア再生滞在時間パネル | メディア再生滞在時間は、ビューアエンゲージメントに関する貴重なインサイトを提供し、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。特定の時点でのメディアストリームの視聴時間を確認できます。再生時間は、新たな 5 分、15 分、30 分の時間粒度を含む、様々な粒度で分割できます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=ja) | 2022年8月9日（PT） |
| モバイルスコアカードで注釈を共有 | ワークスペースで作成された注釈をモバイルスコアカードに表示できます。これにより、組織とキャンペーンに関するコンテキストデータのニュアンスやインサイトを、モバイルスコアカードプロジェクト内で直接共有でき、Analytics ダッシュボードモバイルアプリで表示できます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=ja) | 2022年6月15日 |
| Customer Journey Analytics更新のReport Builder | スケジュールおよびデータブロックマネージャーなどの機能が含まれます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=ja) | 2022年5月18日（PT） |
| ワークスペースの注釈 | Analysis Workspace の注釈を使用すると、コンテキストデータのニュアンスとインサイトを組織に効果的に伝えることができます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=ja) | 2022年3月23日（PT）から順次展開を開始 |
| モバイルスコアカードプロジェクトのプレビューモード | Analytics ダッシュボードアプリにおけるモバイルスコアカードの表示のプレビューを、スコアカードビルダーから直接起動します。プレビューモードを使用すると、アプリ内と同じ方法でフィルターやグラフを操作でき、スコアカードを保存および共有する前にエクスペリエンスをプレビューできます。また、デバイスピッカーをプレビューモードで使用して、様々なデバイスでのスコアカードの表示を確認することもできます。[詳細情報](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=ja#preview) | 2022年2月16日 |


## Adobeストリーミングメディアコレクションの新機能と更新された機能 {#sm-features}

| 機能 | 説明 | ターゲット日 |
| ----------- | ---------- | ------- |
| 複数のプレーヤーの状態トラッキング | Media Collection API を使用して、複数のプレーヤーの状態トラッキングを実装します。[詳細情報](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=ja) | 2022年9月 |
| XDM フィールドの名前を変更しました | 一貫性を保つために次の XDM フィールド名を変更しました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーの状態パラメーター<br>*品質パラメーター | 2022年9月 |
| Device Co-op リファレンス | Adobe Experience Cloud Device Co-op および Experience Cloud ID サービスの要件へのリファレンスを削除しました。 | 2022年8月 |
| コレクションおよびレポートのフィールド名と XDM パスを更新しました | 次のパラメーターが更新されました。<br>*オーディオおよびビデオパラメーター<br>*広告パラメーター<br>*チャプターパラメーター<br>*プレーヤーステートパラメーター<br>*品質パラメーター | 2022年8月 |
| 分平均オーディエンス | Media Analytics のお客様は、分平均オーディエンスパネルを使用すると、コンテンツの平均消費量をより正確に把握できます。<br>分平均オーディエンスを使用すると、あらゆる長さやジャンルのプログラミングを比較できます。さらに、お客様はデジタル分平均オーディエンスを、線形 TV 分平均指標と比較したり、この指標に追加したりできます。このパネルでは、カスタム期間の平均オーディエンスをより柔軟に測定できるほか、期間の分類が更新された場合にも測定できます。[詳細情報](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=ja) | 2022年3月16日（PT） |
| メディア再生滞在時間パネル | メディアユーザーがメディア再生時間パネルを使用して、1 日の閲覧時間に基づいた視聴者数を、指定された精度で把握する方法を説明します。<br>[メディア再生滞在時間パネル（チュートリアル）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=ja) | 2022年1月 |


## *以前のリリースノート*

| 機能 | 説明 | ターゲット日または更新日 |
| ----------- | ---------- | -------------- |
| メディア再生滞在時間 | アドビのストリーミングメディア再生滞在時間は、ビューアのエンゲージメントに関する貴重なインサイトを提供します。これにより、メディア企業は日分割機能を備えた高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関する、より深く、より詳細なインサイトを得ることができます。特定の時点でのメディアストリームの視聴時間を確認できます。再生時間は、様々な粒度（新しい 5 分、15 分、30 分の時間粒度を含む）で分割できます。[詳細情報...](/help/reporting/workspace/media-playback-time-spent.md) | 2021年9月 |
| Analytics Workspace のメディア同時閲覧者パネル | ピーク同時実行が発生した場所、または下降が発生した場所を把握します。コンテンツの質と閲覧者のエンゲージメントに関する貴重なインサイトを取得でき、ボリュームやスケールのトラブルシューティングや計画に役立ちます。[詳細情報…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspace のメディア同時閲覧者パネル（チュートリアル）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=ja#analysis-workspace) | 2020年9月<br><br><br> 2021年1月 |
| サポートされるデバイスとプラットフォーム | AEP SDK を含むメディア Launch 拡張機能で、以下の OTT デバイスがサポートされるようになりました。 <div><ul><li>Apple TV（tvOS）</li><li>Fire TV（Fire OS）</li><li>Android TV</li></ul></div> | 2020年6月 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
