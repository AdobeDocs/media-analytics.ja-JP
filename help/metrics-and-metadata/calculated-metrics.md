---
title: ストリーミングメディアの計算指標
description: アドビのストリーミングメディアの計算指標と指標の数式について説明します。
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 100%

---

# 計算指標{#calculated-metrics}

ストリーミングメディアの計算指標は、平均広告視聴時間やメディアストリームあたりの平均広告数など、ターゲットを絞ったストリーミングメディアデータを取得できるカスタム指標です。

Adobe Analytics の計算指標について詳しくは、Adobe Analytics コンポーネントガイドの[計算指標および高度な計算（派生）指標](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=ja)を参照してください。

>[!NOTE]
>
>これらの計算指標は、2018 年 9 月 13 日に導入されました。

| 指標 | 説明 | 数式 |
|---|---|---|
| メディアストリームあたりの平均広告数 | メディア開始あたりの広告開始 | `Ad Starts / Media Starts` |
| メディアストリームあたりの平均チャプター数 | メディア開始あたりのチャプター開始 | `Chapter Start / Media Starts` |
| 平均メディア視聴時間 | メディア開始あたりの合計視聴時間（HH:MM:SS） | `Media Time Spent / Media Starts` |
| 平均コンテンツ視聴時間 | コンテンツ開始あたりのコンテンツ視聴時間（HH:MM:SS） | `Content Time Spent / Content Start` |
| 平均広告滞在時間 | 広告開始あたりの広告視聴時間（HH:MM:SS） | `Ad Time Spent / Ad Start` |
| 平均チャプター閲覧時間 | チャプター開始あたりのチャプター閲覧時間（HH:MM:SS） | `Chapter Time Spent / Chapter Start` |
| メディア完了率 | メディア開始に対するコンテンツ完了率（％） | `Content Completes/ Media Starts` |
| コンテンツ完了率 | コンテンツ開始に対するコンテンツ完了率（％） | `Content Completes / Content Starts` |
| 広告完了率 | 広告開始に対する広告完了の割合（％） | `Ad Completes / Ad Starts` |
| チャプター完了率 | チャプター開始に対するチャプター完了率（％） | `Chapter Completes / Chapter Starts` |
| 開始前にドロップ率 | メディア開始に対する開始前のドロップ率（％） | `Drops before Starts / Media Starts` |
| コンテンツ一時停止時間率 | コンテンツ視聴時間に対する合計一時停止時間の割合（％） | `Total Pause Duration / Content Time Spent` |
| コンテンツバッファー時間率 | コンテンツ視聴時間に対する合計バッファー時間の割合（％） | `Total Buffer Duration / Content Time Spent` |
| コンテンツ開始時間率 | コンテンツ視聴時間に対する開始までの時間の割合（％） | `Time to Start / Content Time Spent` |
| 広告視聴時間率 | コンテンツ視聴時間に対する広告視聴時間の割合（％） | `Ad Time Spent / Content Time Spent` |
