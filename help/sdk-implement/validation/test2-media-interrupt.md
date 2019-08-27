---
seo-title: Test2メディアの中断
title: Test2メディアの中断
uuid: eeccd534-63fd-4dd3- b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# テスト2:メディア中断{#test-media-interruption}

このテストケースでは、モバイルの中断の動作を検証します。証明書リクエストの必須要素です。

## Certification Request Form

**証明書リクエストフォームを以下からダウンロードします。==&gt;**  [Certification Request Form.](cert_req_form.docx)

## テスト手順

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、次の順序で次の呼び出しが送信されます。

   1. Adobe Analytics（AppMeasurement）の起動
   1. Media Analytics（ハートビート） Start
   1. Media Analytics（ハートビート） Adobe Analytics Start呼び出し要求
   上記の最初の2回の呼び出しには、追加のメタデータと変数が含まれています。パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上記の3回目の呼び出しは、Media SDKがAdobe AnalyticsのStart呼び出し（`pev2=ms_s`）をAdobe Analyticsサーバーに送信することを要求したMedia Analyticsサーバーに通知します。

1. **5分間以上メインコンテンツを再生する**

   **コンテンツの再生**

   コンテンツの再生中、Media SDKは、10秒ごとにMedia Analyticsサーバーにplay呼び出し（ハートビート）を送信します。

   パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **アプリまたはブラウザーをフォアグラウンドに戻す**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **5分間以上メインコンテンツメディアを再生する**

   パラメーターとメタデータの呼び出しについては、「テストコールの詳細」を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **メディアプレイヤーを閉じる**

   メディアプレイヤーを閉じても、追加のトラッキングコールは実行されません。

