---
seo-title: Test2メディアの中断
title: Test2メディアの中断
uuid: eeccd534-63fd-4dd3- b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# テスト2:メディア中断{#test-media-interruption}

このテストケースは、認定リクエストフォームの一部として必要であり、モバイルの中断動作を検証します。

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、次の順序で次の呼び出しが送信されます。

   1. メディア分析開始
   1. ハートビートの開始
   1. ハートビート分析開始
   上記の最初の2回の呼び出しには、追加のメタデータと変数が含まれています。パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md)

1. **5分間以上メインコンテンツメディアを再生する**

   **コンテンツの再生**

   通常のメインコンテンツ再生中には、ハートビート呼び出しが 10 秒間隔でハートビートサーバーに送信されます。

   パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   アプリがバックグラウンドで実行されている間、main:pause 呼び出しのみがハートビートサーバーに送信される必要があります（VHL バージョン 1.6.6 以降）。

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **5分間以上メインコンテンツメディアを再生する**

   パラメーターとメタデータの呼び出しについては、「テストコールの詳細」を参照 [してください。](/help/sdk-implement/validation/test-call-details.md)

1. **メディアプレイヤーを閉じる**

   メディアプレイヤーを閉じても、追加のトラッキングコールは実行されません。

