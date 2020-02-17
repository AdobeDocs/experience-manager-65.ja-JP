---
title: 「チュートリアル：アダプティブフォームの発行」
seo-title: 「チュートリアル：アダプティブフォームの発行」
description: アダプティブフォームをAEMページとして発行し、AEMサイトページに埋め込む、外部Webページにアダプティブフォームを埋め込む
seo-description: アダプティブフォームをAEMページとして発行し、AEMサイトページに埋め込む、外部Webページにアダプティブフォームを埋め込む
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、フォームを発行して、エンドユーザーが使用できるようにすることができます。 エンドユーザーは、発行されたフォームを任意のデバイスおよびインターネットブラウザーで開くことができます。 アダプティブフォームが発行されると、フォームと関連するコンテンツがAEM作成者インスタンスからAEM発行インスタンスにコピーされます。 フォームは、発行インスタンスを通じてエンドユーザーが使用できるようになります。

アダプティブフォームを発行するには、次の方法があります。

* [アダプティブフォームをAEMページとして発行する](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [アダプティブフォームをAEMサイトページに埋め込む](#embed-the-adaptive-form-in-an-aem-sites-page)
* [アダプティブフォームを外部Webページ（AEMの外部でホストされる非AEM webページ）に埋め込む](../../forms/using/publish-your-adaptive-form.md)

## 事前準備 {#before-you-start}

* **[AEM Forms発行インスタンスの設定](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:発行インスタンスは、発行モードで実行されるAEM Formsの公開インスタンスです。 実稼働環境では、発行インスタンスは組織のファイアウォールの外にあります。
* **[レプリケーションと逆レプリケーションの設定](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製は、作成者インスタンスから発行インスタンスにコンテンツをコピーし、発行インスタンスから作成者インスタンスにユーザー入力（例えば、フォーム入力）を返します。

## アダプティブフォームをAEMページとして発行する {#publish-the-adaptive-form-as-an-aem-page}

アダプティブフォームがAEMページとして発行されると、Webページ全体には発行済みのフォームのみが含まれます。 アダプティブフォームのURLを使用して、別のWebページからリンクすることができます。 アダプティブ **フォームをAEMページとして発行するには** 、次の手順を実行します。

1. AEM Forms作成者インスタンスにログインし、AEM Forms UIでshipping-address-add-update-formアダプティブフォームを探します。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 配送先住所 — 追加 — 更新 — フォームアダプティブフォームを選択し、「発行」をタッ **プします**。 アダプティブフォームに関連するアセットを含むダイアログが表示されます。 「**発行**」をタップします。アダプティブフォームが発行され、成功ダイアログが表示されます。
1. 発行インスタンスでフォームを開きます。 エンドユーザーが入力および送信できるフォームです。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## アダプティブフォームをAEMサイトページに埋め込む {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Formsを使用すると、フォーム開発者はアダプティブフォームをAEMサイトページにシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。Webページ上の他の要素のコンテキストを維持し、同時にフォームを操作するのに役立ちます。

AEM formsは、アダプティブフォームをAEMサイトページに埋め込むためのコンポーネントであるAEM formsコンテナを提供します。 デフォルトでは、コンポーネントはAEMサイトコンテナに表示されません。 次の手順を実行して、AEM Forms Containerコンポーネントを有効にし、アダプティブフォームをAEMサイトページに埋め込みます。

1. We.Retailサイトで編集するページを作成し、開きます。 例えば、https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html [です](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 アダプティブフォームはサイトページに埋め込まれます。

   アダプティブフォームを既存のWe.Retailサイトのページに埋め込むこともできます。 例えば、ABOUT US（米国について）ページhttps://localhost:4502/editor.html/content/we-retail/us/en/about-us.htmlのよう [にします](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 これにより、ページを作成する時間を節約できます。 次の手順では、新しく作成されたページを使用します。

   We.Retailサイトは、AEMに付属して出荷されます。 We.Retailサイトがインストールされていない場合は、 [We.Retail Reference Implementationを参照して、サイトをインストールします](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 。

1. 「プロパ ![ティ](assets/properties.png) 」ページ情報をタップし、新しく作成 **したWe.Retailサイトページで「テンプレートの編集** 」オプションを選択します。 ページのテンプレートがブラウザの新しいタブに開きます。
1. レイアウトコンテナボ **ックス内をタップし** 、「feedmanagement」をタ ![ップしま](assets/feedmanagement.png)す。 「許可されて **いるコンポーネント** 」タブで、一般アコ **ーディオンを展開し、** AEM formオプションを選択して **、をタップしま**![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG)す。 AEM Formsコンテナコンポーネントがページに対して有効になっています。

1. 手順1で開いたAEMサイトページを含むブラウザータブを開きます。 「コンポーネント **をここにドラッグ」ボックスをタップし** 、+をタ **ップします。** 「新しいコンポ **ーネントを挿入** 」ボックスで、 **AEM formをタップします。** ページに **AEM Forms Container** コンポーネントが追加されます。
1. 「 **AEM Formsコンテナ」コンポーネントをタップし** 、をタップしま ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/cmppr.png)す。 AEM Formsコンテナのプロパティを含むダイアログボックスが表示されます。 「アセッ **トパス** 」フィールドで、配送先住所 — 追加 — 更新 — フォームアダプティブフォームを参照して選択します。 タップ ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG). アダプティブフォームが ページに埋め込まれました。
1. アダプティブフォームとサイトページの両方を発行します。 次の点について考慮してください。

   * AEMサイトページを初めて発行し、そのページに埋め込みフォームが含まれる場合は、サイトページと埋め込みフォームを発行します。
   * 発行済みサイトページに埋め込まれたフォームのみを変更する場合は、元のフォームを発行し、変更内容は発行済みサイトページに反映されます。 発行されたサイトページにはフォームへの参照情報が含まれているため、ページを再発行する必要はありません。
   * サイトページと埋め込みフォームを変更した場合は、サイトページとフォームを再発行します。
   ![aemサイトに埋め込む](assets/embed-in-aem-sites.png)

   AEMサイトページに「配送先住所と請求先住所の変更」フォームを追加しました。

## 外部Webページにアダプティブフォームを埋め込む {#embed-the-adaptive-form-in-an-external-webpage}

アダプティブフォームは、外部Webページ（AEMの外部でホストされる非AEM webページ）に数行のJavaScriptを挿入することで、外部Webページに埋め込むことができます。 JavaScriptコードは、アダプティブフォームと関連リソースに対してHTTP要求をAEM Formsサーバーに送信し、アダプティブフォームをWebページに追加します。 詳しい手順については、「外部Webペ [ージへのアダプティブフォームの埋め込み」を参照してください](/help/forms/using/embed-adaptive-form-external-web-page.md)。
