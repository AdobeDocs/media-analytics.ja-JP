---
title: ストリーミングメディアコレクションの JSON 検証スキーマ
description: ストリーミングメディアの JSON 検証スキーマを説明し、それを使用してイベントタイプごとに正しいリクエスト本文パラメーターを決定する方法を示します。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 72%

---

# JSON 検証スキーマ {#json-validation-schemas}

ストリーミングメディアコレクションのバックエンドでは、JSON 検証スキーマを使用して、各イベントタイプのリクエストパラメーターを検証します。 これらのスキーマは、ユーザーが利用でき、MA API で使用されているパラメータータイプに関する現在の典拠として機能します。

`GET https://{uri}/api/v1/schemas/{event-type}`

JSON 検証スキーマの使用方法について詳しくは、[イベントリクエストの検証](../mc-api-impl/mc-api-validate-reqs.md)を参照してください。
