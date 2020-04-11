---
title: 「チュートリアル：アダプティブフォームの発行」
seo-title: 「チュートリアル：アダプティブフォームの発行」
description: アダプティブフォームをAEMページとして発行し、AEMサイトページにフォームを埋め込むか、外部Webページにアダプティブフォームを埋め込む
seo-description: アダプティブフォームをAEMページとして発行し、AEMサイトページにフォームを埋め込むか、外部Webページにアダプティブフォームを埋め込む
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、フォームを発行して、エンドユーザーが使用できるようにすることができます。 エンドユーザーは、発行されたフォームを任意のデバイスやインターネットブラウザーで開くことができます。 アダプティブフォームが発行されると、フォームと関連するコンテンツがAEM作成者インスタンスからAEM発行インスタンスにコピーされます。 フォームは、発行インスタンスを通じてエンドユーザーが使用できるようになります。

アダプティブフォームを発行するには、次の方法があります。

* [アダプティブフォームをAEMページとして発行する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [AEMサイトページにアダプティブフォームを埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [アダプティブフォームを外部Webページ（AEMの外部でホストされるAEM以外のWebページ）に埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Forms発行インスタンスの設定](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:発行インスタンスは、発行モードで実行されるAEM Formsの公開インスタンスです。 実稼働環境では、発行インスタンスは組織のファイアウォールの外にあります。
* **[レプリケーションと逆複製の設定](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製は、作成者インスタンスのコンテンツを発行インスタンスにコピーし、発行インスタンスのユーザー入力（フォーム入力など）を作成者インスタンスに返します。

## アダプティブフォームをAEMページとして発行する {#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームがAEMページとして発行されると、Webページ全体には発行済みのフォームのみが含まれます。 アダプティブフォームのURLを使用して、別のWebページからリンクすることができます。 AEMページとし **て配送先住所 — 追加 — 更新 — フォーム** 、アダプティブフォームを発行するには：

1. AEM Forms作成者インスタンスにログインし、AEM Forms UIでshipping-add-update-formアダプティブフォームを見つけます。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 「発送先住所 — 追加 — 更新 — フォーム」アダプティブフォームを選択し、「発行」をタッ **プします**。 アダプティブフォームに関連するアセットを含むダイアログが表示されます。 「**発行**」をタップします。アダプティブフォームが発行され、成功ダイアログが表示されます。
1. 発行インスタンスでフォームを開きます。 エンドユーザーが入力および送信できるフォームです。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## AEMサイトページにアダプティブフォームを埋め込む {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Formsを使用すると、フォーム開発者はアダプティブフォームをAEMサイトページにシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。Webページ上の他の要素のコンテキストを維持し、同時にフォームを操作するのに役立ちます。

AEM Formsは、アダプティブフォームをAEMサイトページに埋め込むためのコンポーネントであるAEM Formsコンテナを提供します。 デフォルトでは、コンポーネントはAEMサイトコンテナに表示されません。 次の手順を実行して、AEM Formsコンテナコンポーネントを有効にし、AEMサイトページにアダプティブフォームを埋め込みます。

1. We.Retailサイトで編集用のページを作成し、開きます。 例えば、 [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 アダプティブフォームはサイトページに埋め込まれます。

   アダプティブフォームを既存のWeb.Retailサイトのページに埋め込むこともできます。 例えば、米国についてのページhttps://localhost:4502/editor.html/content/we-retail/us/en/about-us.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 ページを作成する時間を節約できます。 次の手順では、新しく作成されたページを使用します。

   We.Retailサイトは、AEMに付属して出荷されます。 We.Retailサイトがインストールされていない場合は、 [We.Retail Reference Implementationを参照して、サイトのインストールを参照し](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) てください。

1. 「プロパ ![ティ](assets/properties.png) 」ページ情報をタップし、新しく作成 **したWeb.Retailサイトページで「テンプレートの編集** 」オプションを選択します。 ページのテンプレートがブラウザの新しいタブに開きます。
1. レイアウトコンテナボッ **クス内をタップし** 、「feedmanagement」をタ ![ップしま](assets/feedmanagement.png)す。 「許可され **ているコンポーネント** 」タブで、一般アコ **ーディオンを展開し、** AEM Formオプションを選択して **、をタップしま**![](assets/save_icon.svg)す。 AEM Formsコンテナコンポーネントがページに対して有効になります。

1. 手順1で開いたAEMサイトページを含むブラウザタブを開きます。 「コンポーネントを **ここにドラッグ** 」ボックスをタップし、 **+をタップします。** 「 **Insert New Component** 」ボックスで、 **AEM Formをタップします。** ページ **にAEM Formsコンテナ** ・コンポーネントが追加されます。
1. 「 **AEM Formsコンテナ** 」コンポーネントをタップし ![](assets/configure-icon.svg)ます。 AEM Formsのプロパティを含むダイアログボックスがコンテナします。 「アセッ **トパス** 」フィールドで、「配送先住所 — 追加 — 更新」フォームのアダプティブフォームを参照して選択します。 タップ ![](assets/save_icon.svg). アダプティブフォームが ページに埋め込まれました。
1. アダプティブフォームとサイトページの両方を発行します。 次の点について考慮してください。

   * AEMサイトページを初めて発行し、そのページに埋め込みフォームが含まれる場合は、サイトページと埋め込みフォームを発行します。
   * 発行済みサイトページに埋め込まれたフォームのみを変更する場合は、元のフォームを発行し、変更内容が発行済みサイトページに反映されます。 発行されたサイトページにはフォームへの参照情報が含まれているため、ページを再発行する必要はありません。
   * サイトページと埋め込みフォームを変更した場合は、サイトページとフォームを再発行します。
   ![aemサイトに埋め込む](assets/embed-in-aem-sites.png)

   AEMサイトページに「配送先住所と請求先住所の変更」フォームを追加しました。

## 外部Webページにアダプティブフォームを埋め込む {#embed-the-adaptive-form-in-an-external-webpage}

アダプティブフォームは、外部Webページ（AEMの外部でホストされるAEM以外のWebページ）に埋め込むことができます。この場合、外部WebページにJavaScriptの数行を挿入します。 JavaScriptコードは、アダプティブフォームと関連リソースのHTTP要求をAEM Formsサーバーに送信し、アダプティブフォームをWebページに追加します。 詳しい手順については、「外部Webペ [ージへのアダプティブフォームの埋め込み」を参照してくださ](/help/forms/using/embed-adaptive-form-external-web-page.md)い。
