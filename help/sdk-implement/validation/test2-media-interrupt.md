---
title: テスト2メディア割り込み
description: ここでは、検証で使用されるメディア中断テストについて説明します。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# テスト2:メディアの中断{#test-media-interruption}

このテストケースは、モバイルの中断動作を検証します。 これは、証明書要求の必須要素です。

## 証明書の要請フォーム

**次のURLから証明書申請フォームをダウンロードします。==&gt;**[Certification Request Form.](cert_req_form.docx)

## テスト手順

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、次の呼び出しが次の順序で送信されます。

   1. Adobe Analytics(AppMeasurement)の開始
   1. Media Analytics（ハートビート）開始
   1. Media Analytics（ハートビート）Adobe Analytics start呼び出しの要求
   上記の最初の2つの呼び出しには、追加のメタデータと変数が含まれています。 呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上記の3回目の呼び出しは、Adobe Analytics start呼び出し(`pev2=ms_s`)のAdobe Analyticsサーバーへの送信をMedia SDKが要求したことをMedia Analyticsサーバーに通知します。

1. **メインコンテンツを5分以上中断せずに再生**

   **コンテンツの再生**

   コンテンツの再生中、Media SDKは再生呼び出し（ハートビート）を10秒ごとにMedia Analyticsサーバーに送信します。

   呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **アプリまたはブラウザーを前面へ戻す**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **メインコンテンツメディアを5分以上中断なく再生**

   呼び出しパラメーターとメタデータについては、「呼び出しの詳 [細のテスト」を参照してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **メディアプレイヤーを閉じる**

   メディアプレイヤーが閉じられた後は、追加のトラッキングコールは発生しません。

