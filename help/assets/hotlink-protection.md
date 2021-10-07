---
title: Dynamic Mediaでのホットリンク保護の有効化
description: Dynamic Mediaでホットリンク保護を有効にする方法に関する情報です。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 47%

---

# Dynamic Mediaでのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合におこなわれます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク *保護* は、他の Web サイトが Web ページ上の画像、CSS、JavaScript に直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Experience Managerカスタマ](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support) ーサポートは、CDN(Content Delivery Network) レベルでリファラーフィルターを設定し、ドメインに許可された Web サイトにのみDynamic Mediaコンテンツを提供するようにします。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。ホットリンク保護を有効にするには、管理者がAdobeカスタマーサポートサポートチケットを作成して、Dynamic Mediaアカウントに対する設定の変更をリクエストする必要があります。 ホットリンク保護を有効化するための追加費用は発生しません。
