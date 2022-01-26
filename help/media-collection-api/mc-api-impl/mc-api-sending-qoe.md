---
title: QoE データの送信
description: qoeData JSON キーを使用してイベントを送信する方法について説明します。
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---

# QoE データの送信 {#sending-qoe-data}

すべてのイベントは、JSON リクエスト本文の `qoeData` キーと共に配置される、追加の `params` JSON キーを使用して修飾できます。

>[!NOTE]
>
>[JSON 検証スキーマ](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)を調べて、パラメーターのタイプとそれが必須かオプションかを確認してください。
