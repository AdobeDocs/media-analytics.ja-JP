---
title: セグメント
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# セグメント{#segments}

>[!NOTE]
>
>These reporting segments associated with Media Stream Type were introduced on 9/13/18 along with the `streamType` parameter.

| セグメント | 説明 | ルール |
|---|---|---|
| メディアストリームタイプ：All | すべての&#x200B;*メディア*&#x200B;ストリームデータをセグメント化します。 | 「コンテンツ（ID）が存在する」 |
| メディアストリームタイプ：Audio | すべての&#x200B;*オーディオ*&#x200B;ストリームデータをセグメント化します。 | 「コンテンツ（ID）が存在する」かつ「メディアストリームタイプ = `audio`」 |
| メディアストリームタイプ：Video | すべての&#x200B;*ビデオ*&#x200B;ストリームデータをセグメント化します。 | 「コンテンツ（ID）が存在する」かつ「メディアストリームタイプ ! = `audio`" |
| メディアコンテンツタイプ：VoD | すべての VoD コンテンツをセグメント化します。 | "コンテンツタイプ = `vod`" |
| メディアコンテンツタイプ：Live | すべてのライブコンテンツをセグメント化します。 | "コンテンツタイプ = `live`" |
| メディアコンテンツタイプ：Linear | すべてのリニアコンテンツをセグメント化します。 | "コンテンツタイプ = `linear`" |
| メディアコンテンツタイプ：Podcast | すべてのポッドキャストコンテンツをセグメント化します。 | "コンテンツタイプ = `podcast`" |
| メディアコンテンツタイプ：Audiobook | すべてのオーディオブックコンテンツをセグメント化します。 | "コンテンツタイプ = `audiobook`" |
| メディアコンテンツタイプ：AoD | すべての AoD コンテンツをセグメント化します。 | "コンテンツタイプ = `aod`" |

