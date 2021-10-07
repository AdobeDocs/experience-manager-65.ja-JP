---
title: Dynamic Media Classicを使用したコンテンツ配信ネットワークキャッシュの無効化
description: コンテンツ配信ネットワーク (CDN) にキャッシュされたコンテンツを無効にすると、Dynamic Media Classicで配信されるアセットをすばやく更新できます。キャッシュの有効期限が切れるのを待つ必要はありません。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 58%

---

# Dynamic Media Classicを使用したコンテンツ配信ネットワークキャッシュの無効化 {#invalidating-your-cdn-cached-content}

Dynamic Media アセットは、配信を高速化するために、CDN（コンテンツ配信ネットワーク）によってキャッシュされます。ただし、あるアセットを更新する場合に、変更をすぐに適用したいことがあります。CDN にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。

>[!IMPORTANT]
>
>次の手順は、Adobe Experience Manager 6.5、Service Pack 5(Experience Manager6.5.5) 以前のDynamic Mediaにのみ適用されます。<br>Experience Manager6.5、Service Pack 6(Experience Manager6.5.6) 以降でDynamic Mediaを使用する場合は、「 [Dynamic Mediaを使用した CDN キャッシュの無効化](/help/assets/invalidate-cdn-cache-dynamic-media.md)」に記載されている手順に従います。

[Dynamic Media Classic（Scene7）のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**Dynamic Media Classicを使用して CDN キャッシュを無効にするには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)を開き、アカウントにログインします。

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、Adobeカスタマーサポートにお問い合わせください。

1. ページの右上隅付近で、**[!UICONTROL 設定]** / **[!UICONTROL アプリケーション設定]** / **[!UICONTROL 一般設定]** に移動します。
1. アプリケーションの一般設定ページで、「サーバー」グループ見出しの下にある「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスを見つけます。

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   例えば、次の例にあるように、特定の画像 ID ではなく、`<ID>` を参照する画像 URL（画像プリセットまたは画像の修飾子を含む）を入力するとします。

   `https://server.com/is/image/Company/<ID>?$product$`

   テンプレートに `<ID>` のみが含まれる場合、Dynamic Media によって `https://<server>/is/image` 部分が入力されます。ここで、`<server>` は、一般設定で定義されているパブリッシュサーバー名であり、&lt;ID> は、無効化の対象として選択されたアセットです。

1. ページの右下隅で「**[!UICONTROL 閉じる]**」を選択します。
1. Dynamic Media Classicのユーザーインターフェイスで、1 つ以上のアセットを選択し、**[!UICONTROL File]** / **[!UICONTROL Invalidate CDN]** に移動します。 作成したテンプレートから生成された 1 つ以上の URL と、選択したアセット（またはアセット群）からなるリストが表示されます。このリストに使用されているのは、アプリケーションの一般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル]** / **[!UICONTROL CDN を無効にする]** に移動すると、CDN 無効化のユーザーインターフェイスに、次のように生成された URL が表示されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 「URL」リストボックスで、「**[!UICONTROL Continue]**」を選択して、特定の URL ごとにキャッシュをクリアします。 URL リストボックスでは、URL を入力または貼り付けることによって、URL を編集したり、追加したりできます。事前に CDN 無効化テンプレートを設定する必要はありません。

   「**[!UICONTROL 続行]**」を選択すると、キャッシュのクリアにかかる時間の見積もりを示すインジケーターが表示されます。

   複数のアセットを選択して **[!UICONTROL ファイル]** / **[!UICONTROL CDN を無効にする]** に移動した場合、保存された **[!UICONTROL テンプレートの URL]** で各アセットが参照されます。 したがって、**[!UICONTROL CDN 無効化テンプレート]** を定義し、Web サイトで参照される各 URL の画像プリセット（製品の詳細や検索結果など）を参照できます。 これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択して **[!UICONTROL File]** / **[!UICONTROL Invalidate CDN]** に移動すると、Dynamic Mediaは CDN 無効化テンプレートを使用して、コンテンツ配信ネットワーク (CDN) 内の無効化する URL を自動的に作成します。 「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに何も入力していないと、空白の URL リストが返されます。CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。URL を特定した後は、上記の手順で、それらの URL を「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに追加できます。これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >もう 1 つのオプションとして、完全な URL を **[!UICONTROL CDN 無効化]**&#x200B;リストに追加する方法があります。この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。
