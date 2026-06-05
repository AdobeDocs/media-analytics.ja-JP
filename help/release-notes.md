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
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 36%

---

# ストリーミングメディアサービスのリリースノート

**最終更新**: 2026年6月4日

## 2026

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **サポートスケジュールのデータ** | 過去のライブコンテンツのスケジュールデータをアップロードして、プログラムやセグメント別の視聴者を追跡できます。 サポートされるコンテンツの種類は次のとおりです。<ul><li>FAST（無料広告サポート TV）プラットフォーム</li><li>ローカルストリーム</li><li>ライブスポーツ</li></ul>詳しくは、「[ スケジュール データをアップロードしてライブコンテンツを追跡する](/help/use-cases/track-schedule-data.md) ユースケース」を参照してください。 | ロールアウト開始：2025年10月29日（PT）<p>一般公開：2026年10月</p> |

## 2025年

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **`mediaTimed`XDM フィールドの非推奨化** | `mediaTimed` XDM オブジェクトは、`mediaReporting` フィールドパスのために非推奨（廃止予定）になっています。 2025年5月9日（PT）より前にAnalytics ソースコネクタを実装したお客様は、設定を移行する必要があります。 詳しくは、次の移行ガイドを参照してください。<ul><li>[新しいストリーミングメディアフィールドにオーディエンスを移行](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[新しいストリーミングメディアフィールドを使用するようにCustomer Journey Analyticsを移行](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[ カスタムフィールドのデータ準備を新しいストリーミングメディアフィールドに移行](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[ プロファイルを新しいストリーミングメディアフィールドに移行](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | 2025年10月 |

## 2024

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **Web SDK サポート** | Web SDKまたはWeb SDKタグ拡張機能を使用して、ストリーミングメディア web データをAdobe Experience Platform Edge Networkに送信します。これにより、Customer Journey Analytics、Real-Time CDP、Journey Optimizer、イベント転送などのプラットフォームソリューションをまたいで統合されたコレクション方法が可能になります。 詳しくは、[ ストリーミングメディア用のWeb SDKの設定](/help/implementation/edge/web-sdk.md)または[ ストリーミングメディア用のWeb SDK タグ拡張機能の設定](/help/implementation/edge/web-sdk-tags.md)を参照してください。 | 2024年5月29日（PT） |
| **Roku サポート** | Roku SDKを使用して、Adobe Experience Platformにストリーミングメディアデータを送信します。 詳しくは、[ ストリーミングメディア用にRokuを設定](/help/implementation/edge/roku.md)を参照してください。 | 2024年4月12日（PT） |

## 2023年

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **Experience Edge サポート** | Media Edge APIまたはMobile SDK for iOSおよびAndroidを使用して、ストリーミングメディア収集を実装します。<ul><li>[ ストリーミングメディア用のMedia Edge APIの設定](/help/implementation/edge/media-edge-api.md)</li><li>[ ストリーミングメディア用にiOSを設定](/help/implementation/edge/ios.md)または[ タグ付きストリーミングメディア用にiOSを設定](/help/implementation/edge/ios-tags.md)</li><li>[ ストリーミングメディア用にAndroidを設定](/help/implementation/edge/android.md)または[ タグ付きストリーミングメディア用にAndroidを設定](/help/implementation/edge/android-tags.md)</li></ul> | 2023年5月12日（PT） |

## 2022

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **複数のプレーヤー状態のトラッキング** | メディア コレクション APIを使用して、複数の[ プレーヤー状態トラッキング ](/help/implementation/events/player-state/overview.md)を実装します。 | 2022年9月 |
| XDM フィールドの名前を変更しました | 一貫性のためにXDM フィールド名を変更：<ul><li>オーディオとビデオのパラメーター</li><li>広告パラメーター</li><li>チャプターパラメーター</li><li>プレーヤーステートパラメーター</li><li>品質パラメーター</li></ul> | 2022年9月 |
| **パネルがCustomer Journey Analyticsに追加されました** | Customer Journey Analyticsに[ メディア同時視聴者数パネル ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)と[ メディア再生滞在時間パネル ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)を追加しました。 | 2022年8月9日（PT） |
| **分平均オーディエンス** | [分平均オーディエンス パネル ](https://experienceleague.adobe.com/ja/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)を使用すると、平均コンテンツ消費量をより詳細に把握できます。 <br>分平均オーディエンスを使用すると、あらゆる長さやジャンルのプログラミングを比較できます。 さらに、お客様はデジタル分平均オーディエンスを、線形 TV 分平均指標と比較したり、この指標に追加したりできます。 このパネルでは、カスタム期間の平均オーディエンスをより柔軟に測定できるほか、期間の分類が更新された場合にも測定できます。 | 2022年3月16日（PT） |

## 2021年

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **メディア再生滞在時間** | [再生滞在時間パネル ](https://experienceleague.adobe.com/ja/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)は、視聴者のエンゲージメントに関する貴重なinsightを提供し、メディア組織が日分割の機能を使用した高度な滞在時間分析を通じて、分単位のユーザーエンゲージメントに関するより深く詳細なインサイトを得られるようにします。 特定の時点でのメディアストリームの視聴時間を確認できます。 再生時間は、様々な粒度（新たな 5 分、15 分、30 分の時間粒度を含む）で分割できます。 | 2021年9月 |

## 2020年

| 機能 | 説明 | 日付 |
| --- | --- | --- |
| **メディア同時ビューアパネル** | [同時視聴者数パネル ](https://experienceleague.adobe.com/ja/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)を使用すると、同時視聴数のピークが発生した場所や脱落が発生した場所を把握できます。 コンテンツの質と閲覧者のエンゲージメントに関する貴重なインサイトを取得でき、ボリュームやスケールのトラブルシューティングや計画に役立ちます。<br><br>[ メディア同時視聴者数パネル （チュートリアル） ](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | 2020年9月；2021年1月 |
| **サポートされるデバイスとプラットフォーム** | AEP SDK を含むメディア Launch 拡張機能で、以下の OTT デバイスがサポートされるようになりました。 <div><ul><li>Apple TV（tvOS）</li><li>Fire TV（Fire OS）</li><li>Android TV</li></ul></div> | 2020年6月 |
