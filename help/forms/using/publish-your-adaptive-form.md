---
title: 「チュートリアル：アダプティブフォームの公開」
description: アダプティブフォームを AEM ページとして公開する、AEM Sites ページにフォームを埋め込む、外部 web ページにアダプティブフォームを埋め込む
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 100%

---

# チュートリアル：アダプティブフォームの公開 {#tutorial-publish-your-adaptive-form}

![Hero-image](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)シリーズを構成するチュートリアルです。チュートリアルの使用例全体を理解、実行、デモするために、シリーズを時系列に沿って実施することをお勧めします。

アダプティブフォームの準備が整ったら、エンドユーザーが使用できるようフォームを公開することができます。エンドユーザーは、公開されたフォームを任意のデバイスおよびインターネットブラウザーで開くことができます。アダプティブフォームが公開されると、フォームと関連コンテンツが AEM オーサーインスタンスから AEM パブリッシュインスタンスにコピーされます。このパブリッシュインスタンスを通じて、エンドユーザーはフォームを使用できるようになります。

アダプティブフォームを公開するには、次の方法があります。

* [アダプティブフォームを AEM ページとして公開する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [アダプティブフォームを AEM Sites ページに埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [アダプティブフォームを外部の web ページ（AEM の外部でホストされる AEM 以外の web ページ）に埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Forms パブリッシュインスタンスの設定](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**：パブリッシュインスタンスは、パブリッシュモードで実行される AEM [!DNL Forms] のパブリッシュインスタンスです。実稼動環境では、パブリッシュインスタンスは組織のファイアウォールの外部にあります。
* **[レプリケーションとリバースレプリケーションの設定](https://helpx.adobe.com/jp/experience-manager/6-3/help/sites-deploying/replication.html)**：レプリケーションは、コンテンツをオーサーインスタンスからパブリッシュインスタンスにコピーし、ユーザー入力（フォーム入力など）をパブリッシュインスタンスからオーサーインスタンスに返します。

## アダプティブフォームを AEM ページとして公開する {#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームが AEM ページとして公開された場合、web ページ全体には公開されたフォームのみが含まれます。アダプティブフォームの URL を使用して、別の web ページからリンクすることができます。**shipping-address-add-update-form** アダプティブフォームを AEM ページとして公開するには：

1. AEM [!DNL Forms] オーサーインスタンスにログインし、AEM [!DNL Forms] UI で shipping-address-add-update-form アダプティブフォームを探します。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. shipping-address-add-update-form アダプティブフォームを選択し、「**[!UICONTROL 公開]**」を選択します。アダプティブフォームに関連するアセットを含むダイアログが表示されます。「**[!UICONTROL 公開]**」を選択します。アダプティブフォームが公開され、成功ダイアログが表示されます。
1. パブリッシュインスタンスでフォームを開きます。エンドユーザーがフォームに入力して送信できるようになります。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## アダプティブフォームを AEM Sites ページに埋め込む {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] を使用するとフォーム開発者は、アダプティブフォームをシームレスに AEM [!DNL Sites] ページに埋め込むことができます。埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーは web ページの他の要素に意識を保ちつつ、同時にフォームの操作も行うことができます。

AEM [!DNL Forms] には AEM [!DNL Forms] コンテナという名前のコンポーネントが用意されており、これを使用してアダプティブフォームを AEM [!DNL Sites] ページに埋め込むことができます。デフォルトでは、このコンポーネントは AEM [!DNL Sites] コンテナには表示されません。次の手順を実行して AEM [!DNL Forms] コンテナコンポーネントを有効にし、アダプティブフォームを AEM [!DNL Sites] ページに埋め込みます。

1. We.Retail サイトでページを作成し、編集用に開きます。（例：[https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)）アダプティブフォームが [!DNL Sites] ページに埋め込まれます。

   アダプティブフォームを既存の We.Retail [!DNL Site's] ページに埋め込むこともできます。例えば、「会社概要」ページ（[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)）に埋め込むことができます。これにより、ページを作成する時間を節約できます。以下では、ページを新たに作成する場合の手順を説明します。

   We.Retail サイトは AEM に付属しています。We.Retail サイトをインストールしていない場合は、[We.Retail 参照実装](https://helpx.adobe.com/jp/experience-manager/6-3/help/sites-developing/we-retail.html)を参照してサイトをインストールします。

1. ![プロパティ](assets/properties.png)ページ情報を選択し、新しく作成した We.Retail サイトのページで「**[!UICONTROL テンプレートを編集]**」オプションを選択します。ブラウザーの新しいタブでページのテンプレートが表示されます。
1. 「**[!UICONTROL レイアウトコンテナ]**」ボックス内を選択してから、![feedmanagement](assets/feedmanagement.png) を選択します。「**[!UICONTROL 許可されたコンポーネント]**」タブで、「**[!UICONTROL 一般]**」アコーディオンを展開し、「**[!UICONTROL AEM Form]**」オプションを選択して ![save_icon](assets/save_icon.svg) を選択します。AEM [!DNL Forms] コンテナコンポーネントはそのページに対して有効になっています。

1. 手順 1 で開いた AEM [!DNL Sites] ページを含むブラウザータブを開きます。  「**[!UICONTROL コンポーネントをここにドラッグ]**」ボックスを選択して、**+ を選択します。**「**[!UICONTROL 新しいコンポーネントを挿入]**」ボックス内で、「**[!UICONTROL AEM Form]**」を選択します。この「**[!UICONTROL AEM Forms コンテナ]**」コンポーネントがページに追加されます。
1. **[!UICONTROL AEM Forms コンテナ]**&#x200B;コンポーネントを選択し、![configure-icon](assets/configure-icon.svg) を選択します。AEM [!DNL Forms] コンテナのプロパティを含むダイアログボックス が表示されます。**[!UICONTROL アセットパス]**&#x200B;フィールドで「 shipping-address-add-update-form 」アダプティブフォームを参照して選択してください。![save_icon](assets/save_icon.svg) を選択します。アダプティブフォームがページに埋め込まれました。
1. アダプティブフォームと [!DNL Sites] ページの両方を公開します。次の点について考慮してください。

   * 初めて AEM [!DNL Sites] ページを公開する場合で、かつ、フォームが埋め込まれている場合は、[!DNL Sites] ページに加えて、埋め込まれたフォームも公開してください。
   * 公開されたサイトページに埋め込まれたフォームのみを変更する場合は、元のフォームを公開します。変更内容は、公開されたサイトページに反映されます。公開されたサイトページにはフォームへの参照情報が含まれているため、ページを再公開する必要はありません。
   *  [!DNL Sites] ページと埋め込みフォームに変更を加えた場合、 [!DNL Sites] ページとフォームを再公開します。

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   AEM [!DNL Sites] ページに追加された発送先住所と請求先住所の変更フォーム 。

## 外部 web ページへのアダプティブフォームの埋め込み {#embed-the-adaptive-form-in-an-external-webpage}

外部 web ページに数行の JavaScript を挿入することで、アダプティブフォームを外部 web ページ（AEM の外部でホストされる AEM 以外の web ページ ）に埋め込むことができます。JavaScript コードは、アダプティブフォームおよび関連リソースの HTTP リクエストを AEM [!DNL Forms] サーバーに送信し、アダプティブフォームを web ページに追加します。手順について詳しくは、[外部 web ページへのアダプティブフォームの埋め込み](/help/forms/using/embed-adaptive-form-external-web-page.md)を参照してください。
