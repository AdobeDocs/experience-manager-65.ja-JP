---
title: Dynamic Mediaでのホットリンク保護の有効化
description: Dynamic Mediaでホットリンク保護を有効にする方法に関する情報。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: Business Practitioner, Administrator
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: 設定
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 19%

---

# Dynamic Media{#activating-hotlink-protection-in-dynamic-media}でのホットリンク保護の有効化

ホットリンクとは、サードパーティのWebサイトがHTMLコードを使用してWebサイトの画像を表示する場合です。 訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、他のWebサイトがWebページ上の画像、CSS、またはJavaScriptに直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobe](https://helpx.adobe.com/jp/support.html) サポートでは、転送者のフィルタをCDN(コンテンツ配信ネットワーク)レベルで設定し、Dynamic Mediaのコンテンツがドメインで許可されたWebサイトのリスト上のWebサイトにのみ提供されるようにします。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience ManagerDynamic Mediaにバンドルされている標準搭載のCDNを使用する必要があります。 この機能では、その他のカスタムCDNはサポートされません。 ホットリンク保護を有効にするには、管理者がAdobeカスタマーケアサポートチケットを作成して、Dynamic Mediaアカウントの設定変更をリクエストする必要があります。 ホットリンク保護を有効にするための追加費用は発生しません。
