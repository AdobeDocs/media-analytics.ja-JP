---
title: ストリームタイプ
description: 各メディアセッションがオーディオまたはビデオコンテンツであるかどうかをキャプチャします。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%

---


# ストリームタイプ

>[!BEGINSHADEBOX]

*このページでは、**ストリームタイプ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; ストリームタイプ &#x200B;](/help/implementation/variables/core/stream-type.md)を参照してください。*

>[!ENDSHADEBOX]

**ストリームタイプ** ディメンションは、各メディアセッションがオーディオまたはビデオコンテンツであるかどうかをキャプチャします。 この機能は、レポートスイートで[Media Coreが有効になった後](/help/reporting/media-reports-enable.md)にAdobe Analyticsで利用でき、ストリーミングメディアデータを含むデータセットではCustomer Journey Analyticsで利用できます。

## このディメンションの入力方法

ストリームタイプは、セッション開始時にプレーヤーによって設定され、セッションクローズコールに渡されます。 計算も派生もされていません。 レポートされた値は、収集中に送信された値と正確に一致します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.streamType`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>ストリームタイプが設定されていない場合、ディメンションはそのセッションに入力されません。 これらのセッションは、組み込みのオーディオのみのセグメントおよびビデオのみのセグメントから除外され、ストリームタイプの分類と組み合わせて使用すると、「すべてのストリーミング」メディアセグメントが過小評価されます。

## ディメンション項目

| 値 | 説明 |
| --- | --- |
| `video` | セッションは動画コンテンツで。 |
| `audio` | セッションは、ポッドキャスト、オーディオブック、音楽ストリームなどのオーディオコンテンツでした。 |

カスタム値は、コレクション APIで技術的に受け入れられていますが、推奨されません。 後述の組み込みセグメントと一致しないため、実装全体で一貫性のないレポートが作成される可能性があります。

## 推奨セグメント

ストリームタイプは、Adobe Analyticsの組み込み[!UICONTROL Media Stream Type] セグメントのベースです。 これらのセグメントを使用して、ストリーミングメディアレポートを特定のコンテンツタイプにスコープ付けします。

| セグメント | 規則 |
| --- | --- |
| [!UICONTROL すべてのストリーミングメディア &#x200B;] | コンテンツ （ID）が存在します |
| [!UICONTROL 音声のみ] | コンテンツ （ID）が存在し、ストリームタイプ = `audio` |
| [!UICONTROL &#x200B; ビデオのみ] | コンテンツ （ID）が存在し、ストリームタイプ != `audio` |

>[!TIP]
>
>[!UICONTROL &#x200B; ビデオのみ] セグメントでは、`= video`ではなく`!=` ルールを使用して、ストリームタイプが`audio`以外のカスタム値に設定されている可能性があるセッションを正しくキャプチャします。
