---
title: MVPD
description: ユーザーが認証したケーブル、サテライト、または仮想プロバイダーを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*このページでは、**MVPD**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[MVPD](/help/implementation/variables/standard-metadata/mvpd.md)を参照してください。*

>[!ENDSHADEBOX]

**MVPD** （マルチチャネル ビデオ プログラミング ディストリビューター）ディメンションは、ユーザーがAdobe Pass経由で認証されたプロバイダー（例：`"Comcast"`または`"DirecTV"`）を報告します。 認証プロバイダーによるエンゲージメントを分離するために使用します。

## このディメンションの入力方法

MVPDは、コンテンツがAdobe Passの背後でゲート化されるセッション開始時に、プレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.pass.mvpd`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videomvpd, post_videomvpd` |

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラル MVPD名です。 プロバイダーごとに正規のAdobe Pass MVPD IDを使用すると、プロバイダーごとにデータが1行の項目までロールアップされます。
