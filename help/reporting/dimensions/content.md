---
title: コンテンツ
description: コンテンツ IDでキーを設定して、再生された各メディアの一意の部分をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 5%

---


# コンテンツ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ**のレポートディメンションについて説明します。 この変数の収集方法については、[ コンテンツ ID](/help/implementation/variables/core/content-id.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ** ディメンションは、セッション開始時に設定されたコンテンツ IDにキーを設定して、再生された各ユニークなメディアをレポートします。 これは、ストリーミングメディアのレポート用の主な内訳であり、ビデオ名、ビデオの長さ、アセット ID、最初の放送日、コンテンツの評価などの分類ディメンション用の結合キーです。

## このディメンションの入力方法

コンテンツは、セッション開始時にプレーヤーによって、アセットの安定した識別子として設定されます。 セッションの後続のイベントごとに、同じコンテンツ IDがレポートされます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.name`から自動的に収集されます。 訪問の期間を保持します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `video, post_video` |

>[!IMPORTANT]
>
>コンテンツ IDが必要です。 未設定または空の場合、セッションはストリーミングメディアレポートから削除され、どのメディアレポートにも[!UICONTROL すべてのストリーミングメディア ] セグメントにも表示されません。

## ディメンション項目

各アイテムは、セッション開始時に報告される一意のコンテンツ IDです。 同じアセットのセッションが時間の経過とともに1つの行項目にロールアップされるように、安定したID （内部CMS ID、EIDRやTMS/Gracenoteなどの業界ID、永続的なスラグなど）を使用します。

## 推奨セグメント

| セグメント | 規則 |
| --- | --- |
| [!UICONTROL すべてのストリーミングメディア ] | コンテンツ （ID）が存在します |
