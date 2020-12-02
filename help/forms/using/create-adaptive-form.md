---
title: '"チュートリアル：アダプティブフォームの作成"'
seo-title: '"アダプティブフォームの作成"'
description: このチュートリアルでは、アダプティブフォームの作成方法、レイアウトの設定、プレビューの表示方法について説明します。また、送信操作の設定方法についても説明します。
seo-description: このチュートリアルでは、アダプティブフォームの作成方法、レイアウトの設定、プレビューの表示方法について説明します。また、送信操作の設定方法についても説明します。
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 67%

---


# チュートリアル：アダプティブフォームの作成 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

これは、「[最初のアダプティブフォームを作成する](/help/forms/using/create-your-first-adaptive-form.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて  {#about-the-tutorial}

アダプティブフォームは、動的でレスポンシブな次世代型のフォームです。アダプティブフォームを使用して、エクスペリエンスをカスタマイズすることができます。また、アダプティブフォームを[!DNL Adobe Analytics]と統合して使用状況の統計を確認したり、キャンペーン管理を確認したりすることもできます。 [!DNL Adobe Campaign]アダプティブフォームの機能について詳しくは、「[アダプティブフォームのオーサリングの概要](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

正しい手順を踏めば、フォームの作成と管理を簡単に行うことができます。このチュートリアルでは、以下の操作を行う方法について説明します。

* [顧客が配送先住所を追加するためのアダプティブフォームを作成する](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [顧客の情報を表示して保存するためのアダプティブフォームフィールドのレイアウトを設定する](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [フォームコンテンツが記載された電子メールを送信するためのアクションを作成する](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [アダプティブフォームのプレビューと送信を行う](/help/forms/using/create-adaptive-form.md)

このチュートリアルの最後に、以下のようなフォームにアクセスするためのリンクがあります。\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 手順 1：アダプティブフォームを作成する {#step-create-the-adaptive-form}

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。デフォルトのURLは[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)です。
1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。テンプレートを選択するためのオプションが表示されます。**[!UICONTROL 空白]**&#x200B;テンプレートをタップして選択し、「**[!UICONTROL 次へ]**」をタップします。

1. 「**[!UICONTROL プロパティの追加]**」オプションが表示されます。「**[!UICONTROL タイトル]**」フィールドと「**[!UICONTROL 名前]**」フィールドは入力必須です。

   * **タイトル：「** タイトル」フィールド `Add new or update shipping address` で指定し **** ます。「タイトル」フィールドに入力した値が、フォームの表示名になります。タイトルを指定すると、AEM [!DNL Forms]ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **名前：「名前」フィ** ールド `shipping-address-add-update-form` に **** 指定します。「名前」フィールドに入力した値が、フォームの名前になります。指定された名前のノードがリポジトリに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用することができます。無効な入力はすべてハイフンに置き換えられます。

1. 「**[!UICONTROL 作成]**」をタップします。アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。「**[!UICONTROL 開く]**」をタップして、新しく作成したフォームを新しいタブで開きます。 フォームが編集モードで表示されます。新しく作成されたフォームを必要に応じてカスタマイズするためのサイドバーも表示されます。

   アダプティブフォームのオーサリングインターフェースと使用可能なコンポーネントについて詳しくは、「[アダプティブフォームの作成について](/help/forms/using/creating-adaptive-form.md)」を参照してください。

   ![新たに作成されたアダプティブフォーム](assets/newly-created-adaptive-form.png)

## 手順 2：ヘッダーとフッターを追加する {#step-add-header-and-footer}

AEM [!DNL Forms]は、アダプティブフォーム上に情報を表示するための多くのコンポーネントを提供します。 ヘッダーコンポーネントとフッターコンポーネントを使用すると、フォームの全体的な外観を統一することができます。ヘッダーには通常、会社のロゴ、フォームのタイトル、フォームの概要を指定します。フッターには通常、著作権に関する情報と他のページへのリンクを指定します。

1. ![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png)をタップします。 コンポーネントブラウザーが表示されます。**[!UICONTROL Header]**&#x200B;コンポーネントをコンポーネントブラウザーからアダプティブフォームにドラッグします。
1. 「**[!UICONTROL ロゴ]**」をタップします。ツールバーが表示されます。ツールバーの![aem_6_3_edit](assets/aem_6_3_edit.png)をタップし、「**We.Retail**」と入力して、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

1. 「画像」をタップします。ツールバーが表示されます。![cmppr](assets/cmppr.png)をタップします。 画面の左側にプロパティブラウザーが表示されます。「**[!UICONTROL 参照]**」をタップして、ロゴ画像をアップロードします。![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。 画像がヘッダーに表示されます。

   上記の「Get file」をタップすると、このチュートリアルで使用するロゴをダウンロードすることができます。

   [ファイルを入手](assets/logo.png)

1. **[!UICONTROL フッター]**&#x200B;コンポーネントを![treeexpandall](assets/treeexpandall.png)からアダプティブフォームにドラッグします。 この段階では、フォームは次のようになります。

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 手順 3：情報を取得して表示するためのコンポーネントを追加する {#step-add-components-to-capture-and-display-information}

コンポーネントは、アダプティブフォームを構成するための構築ブロックです。AEM [!DNL Forms]は、アダプティブフォームで情報を取得し、表示するための多くのコンポーネントを提供します。 コンポーネントを![treeexpandall](assets/treeexpandall.png)からフォームにドラッグできます。 使用可能なコンポーネントと対応する機能について詳しくは、「[アダプティブフォームのオーサリングの概要](/help/forms/using/introduction-forms-authoring.md)」を参照してください。

1. **[!UICONTROL 数値ボックスコンポーネント]**&#x200B;をアダプティブフォームにドラッグします。 フッターコンポーネントの前にドロップします。コンポーネントのプロパティを開き、コンポーネントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を&#x200B;**`Customer ID`**&#x200B;に変更し、**[!UICONTROL 要素名]**&#x200B;を&#x200B;**`customer_ID`**&#x200B;に変更し、**[!UICONTROL 必須フィールド]**&#x200B;オプションを有効にして、**[!UICONTROL HTML5番号入力タイプを使用]**&#x200B;をタップします10/>aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。![
1. 3 つのテキストボックスコンポーネントをアダプティブフォームにドラッグし、フッターコンポーネントの前にドロップします。これらのテキストボックスについて、以下のプロパティを設定します。：

   <table> 
    <tbody> 
     <tr> 
      <td><b>Property</b></td> 
      <td><b>テキストボックス 1<br/></b></td> 
      <td><b>テキストボックス 2<br/></b></td> 
      <td><b>テキストボックス 3</b></td> 
     </tr> 
     <tr> 
      <td>タイトル</td> 
      <td>名前<br /> </td> 
      <td>発送先住所</td> 
      <td>都道府県</td> 
     </tr> 
     <tr> 
      <td>要素名</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>必須フィールド</td> 
      <td>Enabled</td> 
      <td>有効</td> 
      <td>有効</td> 
     </tr> 
     <tr> 
      <td>複数行を許可<br /> </td> 
      <td>無効</td> 
      <td>有効</td> 
      <td>無効</td> 
     </tr> 
    </tbody> 
   </table>

1. **[!UICONTROL 数値ボックス]**&#x200B;コンポーネントをフッターコンポーネントの前にドラッグします。コンポーネントのプロパティを開き、次の表に示す値を設定します。![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   | プロパティ | 値 |
   |---|---|
   | タイトル | 郵便番号 |
   | 要素名 | customer_ZIPCode |
   | 最大桁数 | 6 |
   | 必須フィールド | 有効 |
   | 表示パターンタイプ | パターンなし |

1. **[!UICONTROL 電子メール]**&#x200B;コンポーネントをフッターコンポーネントの前にドラッグします。コンポーネントのプロパティを開き、次の表に示す値を設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   | プロパティ | 値 |
   |---|---|
   | タイトル | 電子メール |
   | 要素名 | customer_Email |
   | 必須フィールド | 有効 |

1. **[!UICONTROL 添付ファイル]**&#x200B;コンポーネントをフッターコンポーネントの前にドラッグします。コンポーネントのプロパティを開き、次の表に示す値を設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   <table> 
    <tbody> 
     <tr> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>タイトル</td> 
      <td>Government approved address proof<br /> </td> 
     </tr> 
     <tr> 
      <td>要素名</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>必須フィールド</td> 
      <td>有効</td> 
     </tr> 
    </tbody> 
   </table>

1. **[!UICONTROL 送信ボタン]**&#x200B;コンポーネントをアダプティブフォームにドラッグし、フッターコンポーネントの前にドロップします。コンポーネントのプロパティを開き、「要素名」を`address_addition_update_submit`に変更し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。 これでフォームのレイアウトが設定され、フォームが以下のように表示されます。

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 手順 4：アダプティブフォームの送信アクションを設定する {#step-configure-submit-action-for-the-adaptive-form}

アダプティブフォームの「送信」ボタンをタップすると、送信アクションがトリガーされます。送信アクションを使用して、フォームデータをローカルリポジトリに保存したり、フォームデータを REST エンドポイントに送信したり、フォームデータを電子メールとして送信したりすることができます。アダプティブフォームには、そのほかにも、すぐに使用できる送信アクションがいくつか用意されています。詳しくは、「[送信アクションの設定](/help/forms/using/configuring-submit-actions.md)」を参照してください。

次の手順を使用して、フォームの電子メール送信アクションとデモの送信アクションを設定できます。

1. 電子メールサーバーを設定します。詳しくは、「[電子メール通知の設定](/help/sites-administering/notification.md)」を参照してください。


1. コンテンツブラウザーで「**[!UICONTROL フォームコンテナ]**」をタップし、![cmppr](assets/cmppr.png)をタップします。 プロパティブラウザが左側に開きます。
1. **[!UICONTROL 送信]**／**[!UICONTROL 送信アクション]**&#x200B;に移動します。「**[!UICONTROL 電子メールを送信]**」を選択します。次の値を指定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   | プロパティ | 値 |
   |--- |--- |
   | 送信元 | `donotreply@weretail.com` |
   | To | `${customer_Email}` |
   | 件名 | Acknowledgement: You have added shipping address on We.Retail website. |
   | 電子メールテンプレート | `${customer_Name}`様、次の住所がお客様のアカウントの配送先住所として追加されます。<br>`${customer_Name}`、`${customer_Shipping_Address}`、`${customer_State}`、`${customer_ZIPCode}`<br>よろしくお願いします。Web.Retail |
   | 添付ファイルを含める | 有効 |

   これでフォームが作成されました。フォームのプレビューを表示して機能をテストすることができます。チュートリアルに記載されている名前を使用し、AEM [!DNL Forms]サーバーを実行しているマシン上のフォームにアクセスした場合は、[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)でフォームを利用できます。

## 手順 5：アダプティブフォームのプレビューを表示して、アダプティブフォームを送信する {#step-preview-and-submit-the-adaptive-form}

**[!UICONTROL プレビューオプション]**&#x200B;を使用して、フォームの外観と動作を確認することができます。プレビューモードでフォームを送信し、フォームに適用された検証機能を確認することもできます。例えば、必須フィールドに値が入力されていな場合は、エラーメッセージが表示されます。

アダプティブフォームには、各種のデバイスでフォームの操作性をエミュレートするためのオプションも用意されています。例えば、iPhone、iPad、デスクトップパソコンなどのデバイスについて、エミュレーションを行うことができます。**[!UICONTROL プレビュー]**&#x200B;と&#x200B;**[!UICONTROL エミュレータ]** ![ルーラー](assets/ruler.png)の両方のオプションを組み合わせて使用し、画面サイズの異なるデバイス用のフォームをプレビューできます。

1. フォームエディター右側の「**[!UICONTROL プレビュー]**」オプションをタップします。プレビューモードでフォームが開きます。 このチュートリアルに記載されている値を使用してフォームを作成した場合、フォームのプレビュー URL は [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled) になります。
1. ![ruler](assets/ruler.png)を使用して、様々なデバイスでのフォームの外観を表示します。
1. フォームのフィールドに値を入力して「**[!UICONTROL 送信]**」をタップします。フォームが送信され、デフォルトの「**ありがとうございます**」ページにリダイレクトされます。カスタムの「ありがとうございます」ページを指定することもできます。詳しくは、「[リダイレクトページの設定](/help/forms/using/configuring-redirect-page.md)」を参照してください。

これで、住所を追加するためのアダプティブフォームの準備が完了しました。チュートリアルに記載されている名前を使用し、AEM Formsサーバーを実行しているマシン上のフォームにアクセスした場合は、[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)でフォームを利用できます。
