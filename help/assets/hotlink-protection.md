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
feature: 設定
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 47%

---

# Dynamic Mediaでのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合におこなわれます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、他のWebサイトがWebページ上の画像、CSS、JavaScriptに直接リンクするのを防ぐ方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobeサ](https://helpx.adobe.com/jp/support.html) ポートでは、CDN(Content Delivery Network)レベルでリファラーフィルターを設定し、ドメインに許可されたWebサイトにのみDynamic Mediaコンテンツを提供するようにできます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。ホットリンク保護を有効にするには、管理者がAdobeカスタマーケアサポートチケットを作成して、Dynamic Mediaアカウントに対する設定の変更をリクエストする必要があります。 ホットリンク保護を有効化するための追加費用は発生しません。
