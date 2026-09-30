---
title: メディアストリーミングセグメントの概要
description: メディアストリームタイプのセグメント、説明、ルールなど、メディアストリームタイプに関連付けられているレポートセグメントについて説明します。
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
  - id: c47a19a5-f47b-4e53-afe0-e230da195ebe
    internal-label: Segmentation
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 75%
---
# Streaming Media セグメント

セグメントを使用すると、特性や Web サイトでのインタラクションに基づいて訪問者のサブセットを識別できます。 ストリーミングメディアセグメントを使用すると、オーディオストリーム、ライブストリーム、ポッドキャストストリームなどの訪問者ストリームタイプを識別できます。 Adobe Analytics セグメントについて詳しくは、Adobe Analytics コンポーネントガイドの「[&#x200B; セグメントについて](https://experienceleague.adobe.com/en/docs/analytics/components/segmentation/seg-overview)」を参照してください。

| セグメント | 説明 | 規則 |
|---|---|---|
| メディアストリームタイプ：すべて | すべての&#x200B;*メディア*&#x200B;ストリームデータをセグメント化 | 「コンテンツ（ID）が存在する」 |
| メディアストリームタイプ：オーディオ | すべての&#x200B;*オーディオ*&#x200B;ストリームデータのセグメント化 | 「コンテンツ（ID）が存在する」かつ「メディアストリームタイプ = `audio`」 |
| メディアストリームタイプ：ビデオ | すべての&#x200B;*ビデオ*&#x200B;ストリームデータのセグメント化 | 「コンテンツ（ID）が存在する」かつ「メディアストリームタイプ != `audio`」 |
| メディアコンテンツタイプ：VoD | すべての VoD コンテンツをセグメント化 | 「コンテンツタイプ = `vod`」 |
| メディアコンテンツタイプ：ライブ | すべてのライブコンテンツのセグメント化 | 「コンテンツタイプ = `live`」 |
| メディアコンテンツタイプ：リニア | すべての線形コンテンツのセグメント化 | 「コンテンツタイプ = `linear`」 |
| メディアコンテンツタイプ：ポッドキャスト | すべてのポッドキャストコンテンツのセグメント化 | 「コンテンツタイプ = `podcast`」 |
| メディアコンテンツタイプ：オーディオブック | オーディオブックコンテンツをすべてセグメント化 | 「コンテンツタイプ = `audiobook`」 |
| メディアコンテンツタイプ：AoD | すべての AoD コンテンツのセグメント化 | 「コンテンツタイプ = `aod`」 |
