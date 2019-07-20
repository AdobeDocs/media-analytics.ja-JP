---
seo-title: テスト2ビデオ中断
title: テスト2ビデオ中断
uuid: eeccd534-63fd-4dd3- b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# テスト 2：ビデオの中断{#test-video-interruption}

このテストケースは、認定リクエストフォームの一部として必要であり、モバイルの中断動作を検証します。

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

次の順序でタスクを実行して記録する必要があります。

1. **ビデオプレーヤーの起動**

   ビデオプレーヤーが起動すると、次の順番で次の呼び出しが送信されます。

   1. メディア分析開始
   1. ハートビートの開始
   1. ハートビート分析開始
   上記の最初の2回の呼び出しには、追加のメタデータと変数が含まれています。For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **メインコンテンツビデオを中断せずに 5 分以上再生する**

   **コンテンツの再生**

   通常のメインコンテンツ再生中には、ハートビート呼び出しが 10 秒間隔でハートビートサーバーに送信されます。

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   アプリがバックグラウンドで実行されている間、main:pause 呼び出しのみがハートビートサーバーに送信される必要があります（VHL バージョン 1.6.6 以降）。

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **メインコンテンツビデオを中断せずに 5 分以上再生する**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **ビデオプレーヤーを閉じる**

   ビデオプレーヤーが閉じられた後は、追加のトラッキングコールが発生してはいけません。

