---
title: チュートリアル： アダプティブフォームの発行」
seo-title: チュートリアル： アダプティブフォームの発行」
description: アダプティブフォームをAEMページとして発行したり、AEM Sitesページにフォームを埋め込んだり、外部Webページにアダプティブフォームを埋め込んだりする
seo-description: アダプティブフォームをAEMページとして発行したり、AEM Sitesページにフォームを埋め込んだり、外部Webページにアダプティブフォームを埋め込んだりする
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 9%

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、フォームを発行してエンドユーザーが利用できるようにすることができます。 エンドユーザーは、発行されたフォームを任意のデバイスやインターネットブラウザーで開くことができます。 アダプティブフォームが発行されると、フォームと関連するコンテンツがAEM作成者インスタンスからAEM発行インスタンスにコピーされます。 フォームは、発行インスタンスを通じてエンドユーザーが使用できるようになります。

アダプティブフォームを発行するには、次の方法があります。

* [アダプティブフォームをAEMページとして発行する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [アダプティブフォームをAEM Sitesページに埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [アダプティブフォームを外部Webページ（AEMの外部でホストされているAEM以外のWebページ）に埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Forms発行インスタンスを設定します](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**。 発行インスタンスは、発行モードで実行されているAEM Formsの公開インスタンスです。 実稼働環境では、発行インスタンスは組織のファイアウォールの外にあります。
* **[レプリケーションと逆複製の設定](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**: 複製は、作成者インスタンスのコンテンツを発行インスタンスにコピーし、発行インスタンスのユーザー入力（フォーム入力など）を作成者インスタンスに返します。

## アダプティブフォームをAEMページとして発行する {#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームがAEMページとして発行される場合、Webページ全体には発行済みのフォームのみが含まれます。 アダプティブフォームのURLを使用して、別のWebページからリンクすることができます。 AEMページとして **配送先住所 — 追加 — 更新フォーム** 、アダプティブフォームを発行するには：

1. AEM Forms作成者インスタンスにログインし、AEM FormsUIからshipping-address-add-update-formアダプティブフォームを探します。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 「shipping-add-update-form」アダプティブフォームを選択し、「 **発行**」をタップします。 アダプティブフォームに関連するアセットを含むダイアログが表示されます。 「**発行**」をタップします。アダプティブフォームが発行され、成功ダイアログが表示されます。
1. 発行インスタンスでフォームを開きます。 このフォームは、エンドユーザーが入力および送信できるようにします。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## アダプティブフォームをAEM Sitesページに埋め込む {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Formsを使用すると、フォーム開発者はアダプティブフォームをAEM Sitesページにシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。Webページ上の他の要素のコンテキストに留まり、同時にフォームを操作するのに役立ちます。

AEM Formsには、アダプティブフォームをAEM Sitesページに埋め込むためのコンポーネント、AEM Formsコンテナが用意されています。 デフォルトでは、コンポーネントはAEM Sitesコンテナに表示されません。 次の手順を実行して、AEM Formsコンテナコンポーネントを有効にし、アダプティブフォームをAEM Sitesページに埋め込みます。

1. Web.Retailサイトで、編集するページを作成して開きます。 例えば、https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 アダプティブフォームはサイトページに埋め込まれます。

   アダプティブフォームを既存のWeb.Retailサイトのページに埋め込むこともできます。 例えば、米国についてのページhttps://localhost:4502/editor.html/content/we-retail/us/en/about-us.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 ページを作成する時間を節約できます。 次の手順では、新しく作成されたページを使用します。

   We.RetailサイトはAEMに付属して出荷されます。 We.Retailサイトがインストールされていない場合は、 [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) （We.Retailリファレンスの実装）のインストールを参照してください。

1. 「 ![プロパティ](assets/properties.png) 」ページ情報をタップし、新しく作成したWeb.Retailサイトページで「テンプレート **** を編集」オプションを選択します。 ページのテンプレートがブラウザーの新しいタブに開きます。
1. レイ **アウトコンテナ** ボックス内のをタップし、 ![feedmanagement](assets/feedmanagement.png)をタップします。 「 **許可されるコンポーネント」タブで、** 一般 **アコーディオンを展開し、** AEM Form **オプションを選択して、save_icon**![](assets/save_icon.svg)save_iconComponentsをタップします。 AEM Formsコンテナコンポーネントは、ページに対して有効になります。

1. 手順1で開いたAEM Sitesページを含むブラウザタブを開きます。 「コンポーネントを **ドラッグします** 」ボックスをタップし、 **+をタップします。** 「 **新しいコンポーネントを** 挿入 **」ボックスで、「AEM Form」をタップします。** ページに **AEM Formsコンテナ** コンポーネントが追加されます。
1. 「 **AEM Formsコンテナ** 」コンポーネントをタップし、「 ![設定アイコン](assets/configure-icon.svg)」をタップします。 AEM Formsコンテナのプロパティを含むダイアログボックスが表示されます。 「 **アセットパス** 」フィールドで、アダプティブフォーム「shipping-address-add-update-form」を参照して選択します。 「 ![save_icon](assets/save_icon.svg)」をタップします。 アダプティブフォームが ページに埋め込まれました。
1. アダプティブフォームとサイトページの両方を発行します。 次の点について考慮してください。

   * AEMサイトページを初めて発行する場合で、かつ埋め込みフォームが含まれている場合は、サイトページと埋め込みフォームを発行します。
   * 発行済みサイトページに埋め込まれたフォームのみを変更した場合は、元のフォームを発行し、変更内容が発行済みサイトページに反映されます。 発行されたサイトページにはフォームへの参照情報が含まれているため、ページを再発行する必要はありません。
   * サイトページと埋め込みフォームを変更した場合は、サイトページとフォームを再発行します。

   ![aemサイトに埋め込む](assets/embed-in-aem-sites.png)

   AEM Sitesページに「送付先住所と請求先住所の変更」フォームを追加しました。

## アダプティブフォームを外部Webページに埋め込む {#embed-the-adaptive-form-in-an-external-webpage}

アダプティブフォームは、外部Webページ（AEMの外部でホストされるAEM以外のWebページ）のJavaScriptの行数を外部Webページに挿入することで、外部Webページに埋め込むことができます。 JavaScriptコードは、アダプティブフォームおよび関連リソースのAEM FormsサーバーにHTTP要求を送信し、アダプティブフォームをWebページに追加します。 詳細な手順については、「アダプティブフォームの外部Webページへの [埋め込み](/help/forms/using/embed-adaptive-form-external-web-page.md)」を参照してください。
