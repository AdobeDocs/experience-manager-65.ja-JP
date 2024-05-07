---
title: Dynamic Mediaでのホットリンク保護の有効化
description: Dynamic Media でホットリンク保護を有効化する方法について説明します。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '196'
ht-degree: 100%

---

# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合に行われます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、自社 web サイト上の画像、CSS、JavaScript などに他の web サイトが直接リンクできないようにするための方法です。このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Experience Manager カスタマーサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support)では、コンテンツ配信ネットワーク（CDN）レベルでリファラーフィルターを設定することができます。これにより、ドメインに許可された web サイトにのみ Dynamic Media コンテンツが提供されるようになります。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。ホットリンク保護を有効化するには、Dynamic Media アカウントの設定変更を要求する Adobe カスタマーサポートチケットを管理者が作成する必要があります。ホットリンク保護を有効化するための追加費用は発生しません。
