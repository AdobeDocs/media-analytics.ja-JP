---
seo-title: 再生中のアプリケーション割り込みの処理
title: 再生中のアプリケーション割り込みの処理
uuid: 1ccb4507- bda6-462d- bf67- e22978a4db3d
translation-type: tm+mt
source-git-commit: 8c9592ee7ad97de2cf4aefb226ed1390bc5b53a8

---


# 再生中のアプリケーション割り込みの処理{#handling-application-interrupts-during-playback}

メディアアプリケーション内の再生は、様々な方法で中断できます。ユーザーが一時停止を明示的に押すか、ユーザーがアプリケーションをバックグラウンドに設定したとき。メディアの再生が中断される原因に関係なく、トラッキング手順は同じです。

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. これにより、再生が合計再生時間にカウントされず、以前のプログレスマーカー、セグメントなどが失われてしまいます。Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#section_osf_xqs_h2b}

* _アプリがバックグラウンドになってからセッションが終了するまでどれくらいの時間を確保する必要があります？_

   アプリケーションでバックグラウンド再生が許可されている場合は、API を呼び出すことでトラッキングを続けることができます。すべての通常のトラッキング ping が送信されます。多くのビデオアプリではYouTubeの赤以外のバックグラウンド再生を許可していますが、すべてのオーディオアプリケーションではこれを許可できます。アプリケーションでバックグラウンド再生が許可されていない場合は、一時停止状態に留まり、トラッキングセッションを終了することをお勧めします。アプリケーションは一時停止pingの送信を続行できません。ほとんどの場合、ユーザーがメディアの表示を続行するか、いつ停止するかを判断することができないかどうかを判断できません。また、バックグラウンドで ping を送信し続けるのは不適切なエクスペリエンスでもあります。

* _アプリが長時間バックグラウンドに置かれた後でトラッキングを再開するにはどうするのが適切ですか？_

   アプリケーションは `trackSessionEnd` を呼び出してトラッキングセッションを終了する必要があります。バージョン 2.1 より、SDK は、「終了」ping を送信して、トラッキングセッションが終了したことをバックエンドに通知します。

* _同じセッションを再開するにはどうしたらよいですか？_

   トラッキングセッションを再開するための詳しい手順については、[非アクティブなセッションの再開を参照してください。](../../sdk-implement/cookbook/resuming-inactive.md)SDK は、「再開」ping を送信して、セッションがユーザーによって手動で再開されたことをバックエンドに通知します。

