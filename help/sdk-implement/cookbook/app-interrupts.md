---
title: 再生中のアプリケーション割り込みの処理
description: メディアの再生中にトラッキングが中断された場合の対処方法。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 再生中のアプリケーション割り込みの処理{#handling-application-interrupts-during-playback}

メディアアプリケーションでの再生は、様々な方法で中断できます。ユーザーが一時停止を明示的に押した場合、またはユーザーがアプリケーションをバックグラウンドに置いた場合。 メディアの再生が中断される原因に関係なく、トラッキング手順は同じです。

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. これにより、その時点までの再生が合計再生時間にカウントされず、以前の進行状況マーカーやセグメントなどが失われます。 Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#faq-about-handling-application-interrupts}

* _アプリがバックグラウンドになってからセッションが終了するまでどれくらいの時間を確保する必要があります？_

   アプリケーションでバックグラウンド再生が許可されている場合は、API を呼び出すことでトラッキングを続けることができます。すべての通常のトラッキング ping が送信されます。YouTube red以外のビデオアプリでは、バックグラウンド再生を許可しない場合がありますが、すべてのオーディオアプリで許可されています。 アプリケーションでバックグラウンド再生が許可されていない場合は、1分間一時停止状態のままにしてから、トラッキングセッションを終了することをお勧めします。 アプリケーションは一時停止のpingの送信を続行できません。ほとんどの場合、ユーザーがメディアの閲覧を続行するかどうか、またはユーザーがいつ停止するかを判断できないからです。 また、バックグラウンドで ping を送信し続けるのは不適切なエクスペリエンスでもあります。

* _アプリが長時間バックグラウンドに置かれた後でトラッキングを再開するにはどうするのが適切ですか？_

   アプリケーションは `trackSessionEnd` を呼び出してトラッキングセッションを終了する必要があります。バージョン 2.1 より、SDK は、「終了」ping を送信して、トラッキングセッションが終了したことをバックエンドに通知します。

* _同じセッションを再開するにはどうしたらよいですか？_

   トラッキングセッションを再開するための詳しい手順については、[非アクティブなセッションの再開を参照してください。](/help/sdk-implement/cookbook/resuming-inactive.md)SDK は、「再開」ping を送信して、セッションがユーザーによって手動で再開されたことをバックエンドに通知します。

