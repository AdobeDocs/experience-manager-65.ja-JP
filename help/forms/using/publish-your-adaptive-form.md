---
title: チュートリアル：アダプティブフォームの発行」
seo-title: チュートリアル：アダプティブフォームの発行」
description: アダプティブフォームをAEMページとして発行したり、フォームをAEM Sitesページに埋め込んだり、アダプティブフォームを外部Webページに埋め込んだりする
seo-description: アダプティブフォームをAEMページとして発行したり、フォームをAEM Sitesページに埋め込んだり、アダプティブフォームを外部Webページに埋め込んだりする
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 9%

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、フォームを発行してエンドユーザーが利用できるようにすることができます。 エンドユーザーは、発行されたフォームを任意のデバイスやインターネットブラウザーで開くことができます。 アダプティブフォームが発行されると、フォームと関連するコンテンツがAEM作成者インスタンスからAEM発行インスタンスにコピーされます。 フォームは、発行インスタンスを通じてエンドユーザーが使用できるようになります。

アダプティブフォームを発行するには、次の方法があります。

* [アダプティブフォームをAEMページとして発行する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [AEM Sitesページにアダプティブフォームを埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [アダプティブフォームを外部Webページ(AEMの外部でホストされているAEM以外のWebページ)に埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Forms発行インスタンスを設定します](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**。発行インスタンスは、発行モードで [!DNL Forms] 実行されるAEMの公開インスタンスです。 実稼働環境では、発行インスタンスは組織のファイアウォールの外にあります。
* **[レプリケーションと逆複製の設定](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製は、作成者インスタンスのコンテンツを発行インスタンスにコピーし、発行インスタンスのユーザー入力（フォーム入力など）を作成者インスタンスに返します。

## アダプティブフォームをAEMページとして発行する {#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームがAEMページとして発行される場合、Webページ全体には発行済みのフォームのみが含まれます。 アダプティブフォームのURLを使用して、別のWebページからリンクすることができます。 アダプティブフォーム **をAEMページとして発行するには** 、次の手順に従います。

1. AEM [!DNL Forms] 作成者インスタンスにログインし、AEM [!DNL Forms] UIからshipping-address-add-update-formアダプティブフォームを検索します。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 「shipping-add-update-form」アダプティブフォームを選択し、「 **[!UICONTROL 発行]**」をタップします。 アダプティブフォームに関連するアセットを含むダイアログが表示されます。 「**[!UICONTROL 発行]**」をタップします。アダプティブフォームが発行され、成功ダイアログが表示されます。
1. 発行インスタンスでフォームを開きます。 このフォームは、エンドユーザーが入力および送信できるようにします。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEM Sitesページにアダプティブフォームを埋め込む {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] を使用すると、フォーム開発者はアダプティブフォームをAEM [!DNL Sites] ページにシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。Webページ上の他の要素のコンテキストに留まり、同時にフォームを操作するのに役立ちます。

AEM [!DNL Forms] は、アダプティブフォームをAEM [!DNL Forms] ページに埋め込むためのコンポーネント、AEM [!DNL Sites] コンテナを提供します。 デフォルトでは、コンポーネントはAEM [!DNL Sites] コンテナに表示されません。 次の手順を実行してAEM [!DNL Forms] コンテナコンポーネントを有効にし、アダプティブフォームをAEM [!DNL Sites] ページに埋め込みます。

1. Web.Retailサイトで、編集するページを作成して開きます。 例えば、https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 The adaptive form is embedded to the [!DNL Sites] page.

   アダプティブフォームを既存のWeb.Retail [!DNL Site's] ページに埋め込むこともできます。 例えば、米国についてのページhttps://localhost:4502/editor.html/content/we-retail/us/en/about-us.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 ページを作成する時間を節約できます。 次の手順では、新しく作成されたページを使用します。

   We.RetailサイトはAEMに付属して出荷されます。 We.Retailサイトがインストールされていない場合は、 [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) （We.Retailリファレンスの実装）のインストールを参照してください。

1. 「 ![プロパティ](assets/properties.png) 」ページ情報をタップし、新しく作成したWeb.Retailサイトページで「テンプレート **** を編集」オプションを選択します。 ページのテンプレートがブラウザーの新しいタブに開きます。
1. レイ **[!UICONTROL アウトコンテナ]** ボックス内のをタップし、 ![feedmanagement](assets/feedmanagement.png)をタップします。 「 **[!UICONTROL 許可されるコンポーネント]** 」タブで、 **[!UICONTROL 一般アコーディオンを展開し、「AEM Form]** 」オプションを選択し、「 ****![](assets/save_icon.svg)save_icon」をタップします。 AEM [!DNL Forms] コンテナコンポーネントがページに対して有効になっています。

1. 手順1で開いたAEM [!DNL Sites] ページを含むブラウザータブを開きます。 「コンポーネントを **[!UICONTROL ドラッグします]** 」ボックスをタップし、 **+をタップします。** 「 **[!UICONTROL 新しいコンポーネントを]** 挿入 **[!UICONTROL 」ボックスで、「]** AEM Form」をタップします。 ページに **[!UICONTROL AEM Formsコンテナ]** コンポーネントが追加されます。
1. 「 **[!UICONTROL AEM Formsコンテナ]** 」コンポーネントをタップし、「 ![設定アイコン](assets/configure-icon.svg)」をタップします。 AEM [!DNL Forms] コンテナのプロパティを持つダイアログボックスが表示されます。 「 **[!UICONTROL アセットパス]** 」フィールドで、アダプティブフォーム「shipping-address-add-update-form」を参照して選択します。 「 ![save_icon](assets/save_icon.svg)」をタップします。 アダプティブフォームが ページに埋め込まれました。
1. アダプティブフォームと [!DNL Sites] ページの両方を発行します。 次の点について考慮してください。

   * If you publish the AEM [!DNL Sites] page for the first time and it includes an embedded form, publish the [!DNL Sites] page and the embedded form.
   * 発行済みサイトページに埋め込まれたフォームのみを変更した場合は、元のフォームを発行し、変更内容が発行済みサイトページに反映されます。 発行されたサイトページにはフォームへの参照情報が含まれているため、ページを再発行する必要はありません。
   * ページと埋め込みフォームを変更した場合 [!DNL Sites] は、ページとフォームを再発行し [!DNL Sites] ます。

      ![aemサイトに埋め込む](assets/embed-in-aem-sites.png)
   AEM [!DNL Sites] ページに送料および請求先住所の変更フォームを追加しました。

## アダプティブフォームを外部Webページに埋め込む {#embed-the-adaptive-form-in-an-external-webpage}

アダプティブフォームは、外部WebページにJavaScriptの数行を挿入することで、外部Webページ(AEMの外部でホストされているAEM以外のWebページ)に埋め込むことができます。 JavaScriptコードは、アダプティブフォームおよび関連リソースのHTTP要求をAEM [!DNL Forms] サーバーに送信し、アダプティブフォームをWebページに追加します。 詳細な手順については、「アダプティブフォームの外部Webページへの [埋め込み](/help/forms/using/embed-adaptive-form-external-web-page.md)」を参照してください。
