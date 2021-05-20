---
title: '"チュートリアル：アダプティブフォームをパブリッシュする」'
seo-title: '"チュートリアル：アダプティブフォームをパブリッシュする」'
description: アダプティブフォームをAEMページとして発行する、AEM Sitesページにフォームを埋め込む、外部のWebページにアダプティブフォームを埋め込む
seo-description: アダプティブフォームをAEMページとして発行する、AEM Sitesページにフォームを埋め込む、外部のWebページにアダプティブフォームを埋め込む
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: アダプティブフォーム
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 10%

---

# チュートリアル：アダプティブフォーム{#tutorial-publish-your-adaptive-form}を発行します。

![](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、フォームを発行して、エンドユーザーが使用できるようにすることができます。 エンドユーザーは、公開されたフォームを任意のデバイスおよびインターネットブラウザーで開くことができます。 アダプティブフォームが発行されると、フォームと関連コンテンツがAEMオーサーインスタンスからAEMパブリッシュインスタンスにコピーされます。 フォームは、パブリッシュインスタンスを通じてエンドユーザーに提供されます。

アダプティブフォームを発行するには、次の方法があります。

* [アダプティブフォームをAEMページとして発行する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [アダプティブフォームをAEM Sitesページに埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [外部のWebページ(AEMの外部でホストされる非AEM Webページ)にアダプティブフォームを埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Formsパブリッシュインスタンスを設定します](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**。パブリッシュインスタンスは、パブリッシュモードで実行されているAEMのパブ [!DNL Forms] リックインスタンスです。実稼動環境では、パブリッシュインスタンスは組織のファイアウォールの外にあります。
* **[レプリケーションとリバースレプリケーションの設定](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:レプリケーションは、コンテンツをオーサーインスタンスからパブリッシュインスタンスにコピーし、パブリッシュインスタンスからオーサーインスタンスにユーザー入力（フォーム入力など）を返します。

## アダプティブフォームをAEMページとして発行する{#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームがAEM Pageとして発行されると、Webページ全体には発行されたフォームのみが含まれます。 アダプティブフォームのURLを使用して、別のWebページからリンクすることができます。 **shipping-address-add-update-form**&#x200B;アダプティブフォームをAEMページとして発行するには、次の手順を実行します。

1. AEM [!DNL Forms]オーサーインスタンスにログインし、AEM [!DNL Forms] UIでshipping-address-add-update-formアダプティブフォームを探します。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. shipping-address-add-update-formアダプティブフォームを選択して「**[!UICONTROL 発行]**」をタップします。 アダプティブフォームに関連するアセットを含むダイアログが表示されます。 「**[!UICONTROL 発行]**」をタップします。アダプティブフォームが発行され、成功ダイアログが表示されます。
1. パブリッシュインスタンスでフォームを開きます。 エンドユーザーが入力および送信できるフォームです。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEM Sitesページにアダプティブフォームを埋め込む{#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms]を使用すると、フォーム開発者はアダプティブフォームをAEM [!DNL Sites]ページにシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーはWebページ上の他の要素のコンテキストを維持し、同時にフォームを操作できます。

AEM [!DNL Forms]は、アダプティブフォームをAEM [!DNL Sites]ページに埋め込むためのコンポーネントAEM [!DNL Forms]コンテナを提供します。 デフォルトでは、このコンポーネントはAEM [!DNL Sites]コンテナに表示されません。 次の手順を実行して、AEM [!DNL Forms]コンテナコンポーネントを有効にし、アダプティブフォームをAEM [!DNL Sites]ページに埋め込みます。

1. We.Retailサイトでページを作成し、編集用に開きます。 例えば、[https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)のようにします。 アダプティブフォームが[!DNL Sites]ページに埋め込まれます。

   アダプティブフォームを既存のWe.Retail [!DNL Site's]ページに埋め込むこともできます。 例えば、ABOUT USページ[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)などです。 ページを作成する時間を節約できます。 以下の手順では、新しく作成されたページを使用します。

   We.Retailサイトは、AEMと共に出荷されます。 We.Retailサイトがインストールされていない場合は、 [We.Retail参照実装](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html)へのインストールを参照してください。

1. ![properties](assets/properties.png)ページ情報をタップし、新しく作成したWe.Retailサイトページで「**[!UICONTROL Edit Template]**」オプションを選択します。 ブラウザーの新しいタブにページのテンプレートが開きます。
1. **[!UICONTROL レイアウトコンテナ]**&#x200B;ボックス内をタップし、![feedmanagement](assets/feedmanagement.png)をタップします。 「**[!UICONTROL 許可されるコンポーネント]**」タブで、「**[!UICONTROL 一般]**」アコーディオンを展開し、「**[!UICONTROL AEM Form]**」オプションを選択して、![save_icon](assets/save_icon.svg)をタップします。 AEM [!DNL Forms]コンテナコンポーネントがページに対して有効になっている。

1. 手順1で開いたAEM [!DNL Sites]ページを含むブラウザータブを開きます。 「**[!UICONTROL コンポーネントをここにドラッグ]**」ボックスをタップし、**+をタップします。** 「新規コンポー **[!UICONTROL ネントを挿]** 入」ボックスで、「 **[!UICONTROL AEM Form]**」をタップします。**[!UICONTROL AEM Formsコンテナ]**&#x200B;コンポーネントがページに追加されます。
1. **[!UICONTROL AEM Formsコンテナ]**&#x200B;コンポーネントをタップし、![configure-icon](assets/configure-icon.svg)をタップします。 AEM [!DNL Forms]コンテナのプロパティを含むダイアログボックスが表示されます。 「**[!UICONTROL アセットのパス]**」フィールドで、「 shipping-address-add-update-form 」アダプティブフォームを参照して選択します。 ![save_icon](assets/save_icon.svg)をタップします。 アダプティブフォームが ページに埋め込まれました。
1. アダプティブフォームと[!DNL Sites]ページの両方を発行します。 次の点について考慮してください。

   * AEM [!DNL Sites]ページを初めて発行し、埋め込みフォームが含まれている場合は、[!DNL Sites]ページと埋め込みフォームを発行します。
   * 発行済みサイトページに埋め込まれたフォームのみを変更する場合は、元のフォームを発行し、変更内容が発行済みサイトページに反映されます。 発行されたサイトページにはフォームへの参照情報が含まれているため、ページを再発行する必要はありません。
   * [!DNL Sites]ページと埋め込まれたフォームを変更した場合は、[!DNL Sites]ページとフォームを再発行します。

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   配送先住所と請求先住所の変更フォームがAEM [!DNL Sites]ページに追加されました。

## 外部のWebページにアダプティブフォームを埋め込む{#embed-the-adaptive-form-in-an-external-webpage}

外部Webページに数行のJavaScriptを挿入することで、外部Webページ(AEMの外部でホストされるAEM以外のWebページ)にアダプティブフォームを埋め込むことができます。 JavaScriptコードは、アダプティブフォームおよび関連リソースのHTTPリクエストをAEM [!DNL Forms]サーバーに送信し、アダプティブフォームをWebページに追加します。 詳しい手順については、「 [外部Webページへのアダプティブフォームの埋め込み](/help/forms/using/embed-adaptive-form-external-web-page.md) 」を参照してください。
