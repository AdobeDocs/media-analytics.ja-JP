---
title: QoE データの送信
description: qoeData JSONキーを使用してイベントを送信する方法について説明します。
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# QoE データの送信{#sending-qoe-data}

すべてのイベントは、JSON リクエスト本文の `qoeData` キーと共に配置される、追加の `params` JSON キーを使用して修飾できます。

>[!NOTE]
>
>[JSON 検証スキーマ](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)を調べて、パラメーターのタイプとそれが必須かオプションかを確認してください。
