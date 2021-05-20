---
title: Dynamic Media Classic を使用した CDN キャッシュの無効化
description: CDN（コンテンツ配信ネットワーク）にキャッシュされたコンテンツを無効にすると、Dynamic Media Classicで配信されるアセットをすばやく更新できます。キャッシュの期限が切れるのを待つ必要はありません。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDNキャッシュ，Dynamic Media Classic
role: Business Practitioner, Administrator
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 48%

---

# Dynamic Media Classic を使用した CDN キャッシュの無効化 {#invalidating-your-cdn-cached-content}

Dynamic Mediaのアセットは、CDN（コンテンツ配信ネットワーク）によってキャッシュされ、高速配信が可能です。 ただし、アセットを更新する場合は、変更をすぐに有効にする必要があります。 CDNにキャッシュされたコンテンツを無効にすると、Dynamic Mediaによって配信されるアセットを、キャッシュの期限切れを待たずにすばやく更新できます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。 その他のカスタムCDNは、この機能ではサポートされません。

>[!IMPORTANT]
>
>次の手順は、AEM 6.5、Service Pack 5(AEM 6.5.5)以前のDynamic Mediaにのみ適用されます。<br>AEM 6.5、Service Pack 6(AEM 6.5.6)以降でDynamic Mediaを使用する場合は、「 Dynamic Mediaを使用したCDNキャッシュの無効化」に記載されている手順に従いま [す。](/help/assets/invalidate-cdn-cache-dynamic-media.md)

[Dynamic Media Classic（Scene7）のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**Dynamic Media Classicを使用してCDNキャッシュを無効にするには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app)を開き、アカウントにログインします。

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. ページの右上隅付近にある&#x200B;**[!UICONTROL 設定/アプリケーション設定/一般設定をタップします。]**
1. アプリケーションの一般設定ページで、「サーバー」グループ見出しの下にある「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスを見つけます。

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   例えば、次の例にあるように、特定の画像 ID ではなく、`<ID>` を参照する画像 URL（画像プリセットまたは画像の修飾子を含む）を入力するとします。

   `https://server.com/is/image/Company/<ID>?$product$`

   テンプレートに`<ID>`のみが含まれる場合、Dynamic Mediaは`https://<server>/is/image`を入力します。ここで、`<server>`は一般設定で定義されているパブリッシュサーバー名で、&lt;ID>は無効にするように選択されたアセットです。

1. ページの右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。
1. Dynamic Media Classicユーザーインターフェイスで、1つ以上のアセットを選択し、**[!UICONTROL ファイル/CDNを無効にするをクリックします。]** 作成したテンプレートと選択したアセットから生成された1つ以上のURLのリストが表示されます。このリストに使用されているのは、アプリケーションの一般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップすると、CDN無効化のユーザーインターフェイスに次のように生成されたURLが表示されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 「URL」リストボックスで、「**[!UICONTROL Continue]**」をタップして、特定のURLごとにキャッシュをクリアします。 URLを編集するか、URLリストボックスにURLを入力または貼り付けてURLを追加できます。事前にCDN無効化テンプレートを設定しておく必要はありません。

   「**[!UICONTROL 続行]**」をクリックすると、キャッシュの消去にかかる時間の概算を示すインジケーターが表示されます。

   複数のアセットを選択し、**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップした場合、保存された&#x200B;**[!UICONTROL テンプレートのURLで各アセットが参照されます。]** したがって、各URLの画像プ **[!UICONTROL リセット（製品の詳細や検索結果など）を参照するCDN無効化テンプレートを定義]** し、その画像プリセットをWebサイトで参照できます。これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、Dynamic Media が CDN 無効化テンプレートを使用して、コンテンツ配信ネットワーク（CDN）内の無効化する URL 群を自動的に作成します。「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに何も入力していないと、空白の URL リストが返されます。CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。URL を特定した後は、上記の手順で、それらの URL を「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに追加できます。これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >もう 1 つのオプションとして、完全な URL を **[!UICONTROL CDN 無効化]**&#x200B;リストに追加する方法があります。この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。
