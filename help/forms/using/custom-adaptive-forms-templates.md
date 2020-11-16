---
title: カスタムアダプティブフォームのテンプレートの作成
seo-title: カスタムアダプティブフォームのテンプレートの作成
description: この記事では、カスタムアダプティブフォームのテンプレートの作成方法を説明します。
seo-description: この記事では、カスタムアダプティブフォームのテンプレートの作成方法を説明します。
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 74%

---


# カスタムアダプティブフォームのテンプレートの作成{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms に、動的なテンプレートが導入されました。AEM サイトのテンプレートエディターを使用して、[動的なテンプレートの作成や編集](../../forms/using/template-editor.md)を行うことができます。この記事で説明するテンプレートは、静的なテンプレートです。デフォルトのインストール環境で静的なテンプレートを使用することはできません。[互換性パッケージ](../../forms/using/compatibility-package.md) をインストールして、お使いの環境にこれらのテンプレートを取得します。

## 前提条件 {#prerequisites}

* Understanding of AEM [Page Template](/help/sites-authoring/templates.md) and [Adaptive Form Authoring](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* AEM [クライアント側ライブラリ](/help/sites-developing/clientlibs.md)に関する知識

## アダプティブフォームテンプレート {#adaptive-form-template}

アダプティブフォームテンプレートは、アダプティブフォームの作成に使用される特定のプロパティとコンテンツ構造を持つ特殊な AEM ページテンプレートです。このテンプレートのレイアウト、スタイル、基本的な初期コンテンツ構造は事前に設定されています。

フォームを作成すると、元のテンプレートのコンテンツ構造に対する変更はフォームに反映されません。

## デフォルトのアダプティブフォームテンプレート {#default-adaptive-form-templates}

AEM QuickStart では、次のアダプティブフォームテンプレートを提供します。

* 調査テンプレート:複数の列が設定されたレスポンシブレイアウトを使用して、単一ページのアダプティブフォームを作成できます。 フォームを表示させる画面サイズに基づいてレイアウトは自動で調整されます。
* シンプルな登録テンプレート：ウィザードのレイアウトを使用して複数手順のアダプティブフォームを作成できます。 このレイアウトでは、各手順の完了に必要な式を指定できます。指定した式は、次の手順にウィザードを進める前に検証されます。
* タブ付き登録テンプレート：タブが左側にあるレイアウトを使用して複数タブのアダプティブフォームを作成し、任意の順序でタブにアクセスできるようにします。
* 高度な登録テンプレート：複数のタブとウィザードを使用してフォームを作成します。タブが左側にあるレイアウトを使用し、任意の順序でタブにアクセスできるようにします。署名と検証には Adobe Document Cloud eSign サービスを使用します。
* 空白のテンプレート：ヘッダー、フッター、初期コンテンツのないフォームを作成します。テキストボックス、ボタン、画像などのコンポーネントを追加できます。空白テンプレートでは、[AEM サイトページに埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md)ことができるフォームを作成します。

これらのテンプレートでは、`sling:resourceType` プロパティが、対応するページのコンポーネントに設定されています。ページコンポーネントは、アダプティブフォームのコンテナを含む CQ ページをレンダリングすることでアダプティブフォームをレンダリングします。

次の表では、テンプレートとページコンポーネントの関係を列挙します。

<table>
 <tbody>
  <tr>
   <td><p><strong>テンプレート</strong></p> </td>
   <td><p><strong>ページコンポーネント</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## テンプレートエディターを使用したアダプティブフォームテンプレートの作成 {#creating-an-adaptive-form-template-using-template-editor}

テンプレートエディターを使用して、アダプティブフォームの構造と初期コンテンツを指定できます。 例えば、すべての作成者が、登録フォーム内でテキストボックスを少なくし、ナビゲーションボタンと送信ボタンを設置するようにできます。作成者が他の登録フォームと統一のとれたフォームを作成できるようにするためのテンプレートを作成できます。AEM テンプレートエディターでは次のことが行えます。

* 構造レイヤーでフォームのヘッダーおよびフッターコンポーネントを追加できます。
* フォームの初期コンテンツを提供できます。
* テーマを指定できます。
* 送信、リセット、移動などの操作を指定できます。

For more informtion, see [Template Editor](../../forms/using/template-editor.md).

## CRXDE からのアダプティブフォームテンプレートの作成 {#creating-an-adaptive-form-template-from-crxde}

あらかじめ用意されたテンプレートを使う代わりに、自分でテンプレートを作成してアダプティブフォームの作成に使用することもできます。カスタムテンプレートは、アダプティブフォームのコンテナのほか、ヘッダー、フッターなど、ページ要素を参照するさまざまなページコンポーネントに基づいています。

これらのコンポーネントは Web サイト向けの基本ページコンポーネントを使用して作成することができます。または、あらかじめ用意されたテンプレートで使用されるアダプティブフォームのページコンポーネントを拡張することもできます。

simpleEnrollmentTemplate などのカスタムテンプレートを作成するには、次の手順を実行します。

1. 自分のオーサーインスタンスで CRXDE Lite に移動します。

1. /apps ディレクトリの下に、自分のアプリケーションのフォルダー構造を作成します。例えば、アプリケーションの名前が mycompany の場合、その名前のフォルダーを作成します。通常、アプリケーションフォルダーには components、configuration、templates、src、installation のディレクトリが含まれます。この例では、components、configuration、templates の各フォルダーを作成します。

1. /libs/fd/af/templates フォルダーに移動します。
1. Copy the `simpleEnrollmentTemplate` node.
1. /apps/mycompany/templates フォルダーに移動します。右クリックして「**[!UICONTROL 貼り付け]**」を選択します。
1. 必要に応じて、コピーしたテンプレートノードの名前を変更します。例えば、enrollment-template などに変更します。

1. /apps/mycompany/templates/enrollment-template に移動します。

1. Modify the `jcr:title` and `jcr:description` properties for the `jcr:content` node to distinguish the template from the template you copied.

1. The `jcr:content` node of the modified template contains the `guideContainer` and `guideformtitle` components. `guideContainer` はアダプティブフォームを格納するコンテナです。`guideformtitle` コンポーネントは、アプリケーション名や説明などを表示します。

   `guideformtitle` の代わりに、カスタムコンポーネントまたは `parsys` コンポーネントを含めることができます。例えば、`guideformtitle` を削除して、カスタムコンポーネントまたは `parsys` コンポーネントのノードを含めることができます。コンポーネントの `sling:resourceType` プロパティの参照先が、そのコンポーネントになっていることを確認してください。ページ `component.jsp` ファイルでも同様に定義されます。

1. /apps/mycompany/templates/enrollment-template/jcr:content に移動します。

1. 「**[!UICONTROL プロパティ]**」タブを開き、`cq:designPath` プロパティの値を /etc/designs/mycompany に変更します。

1. 次に、`cq:Page` タイプに /etc/designs/mycompany のノードを作成します。

## アダプティブフォームのページコンポーネントの作成 {#create-an-adaptive-form-page-component}

テンプレートの参照先は /libs/fd/af/components/page/base のページコンポーネントに設定されているため、カスタムテンプレートはデフォルトのテンプレートと同じスタイルを持ちます。コンポーネントの参照は、/apps/mycompany/templates/enrollment-template/jcr:content ノードで定義された `sling:resourceType` プロパティで検索できます。baseはコア製品コンポーネントなので、このコンポーネントを変更しないでください。

1. Navigate to the node /apps/mycompany/templates/enrollment-template/jcr:content and modify the value of the property `sling:resourceType` to /apps/mycompany/components/page/enrollmentpage
1. /libs/fd/af/components/page/base のノードを /apps/mycompany/components/page フォルダーにコピーします。

1. コピーしたコンポーネントの名前を `enrollmentpage` に変更します。

1. **（コンテンツページを既に持っている場合のみ）** Webサイトに既存の `contentpage`コンポーネントがある場合は、次の手順(a ～ d)を実行します。 自分の Web サイトに `contentpage` コンポーネントが存在しない場合は、`resourceSuperType` プロパティを OOTB の基本ページにポイントしたままにすることができます。

   1. For the `enrollmentpage` node, set value of the property `sling:resourceSuperType` to mycompany/components/page/contentpage. `contentpage` コンポーネントは、自分のサイトの基本ページコンポーネントです。他のページコンポーネントで拡張することができます。Remove script files under `enrollmentpage`, except `head.jsp`, `content.jsp`, and `library.jsp`. The `sling:resourceSuperType` component, which is `contentpage` in this case, includes all such scripts. ナビゲーションバーやフッターなどを含むヘッダー類は、`contentpage` コンポーネントから継承されます。

   1. Open the file `head.jsp`.

      The JSP file contains the line `<cq.include script="library.jsp"/>`.

      `library.jsp` ファイルには、`guide.theme.simpleEnrollment` のクライアントライブラリが含まれ、その中にアダプティブフォームのスタイル設定が含まれています。

      The page component `enrollmentpage` has an exclusive `head.jsp` file that overrides the `head.jsp` file of the `contentpage` component.

   1. Include all scripts in the `head.jsp` file for the `contentpage` component to the `head.jsp` file for the `enrollmentpage` component.
   1. `content.jsp` スクリプトの中に、追加のページコンテンツまたはページがレンダリングされる際に含まれる他のコンポーネントへの参照を追加することができます。例えば、`applicationformheader` カスタムコンポーネントを追加する場合、JSP ファイルのコンポーネントに次の参照を追加します。

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同様に、テンプレートのノード構造に `parsys` コンポーネントを追加する場合、カスタムコンポーネントも含めます。

## アダプティブフォームのクライアントライブラリの作成 {#creating-an-adaptive-form-client-library}

The `head.jsp` file of the `enrollmentpage` component for the new template includes a client library `guide.theme.simpleEnrollment`. デフォルトのテンプレートは、このクライアントライブラリも使用します。これらの方法のいずれかを使用して、新しいテンプレートのスタイルを変更します。

* カスタムテーマを定義し、デフォルトのテーマ `guide.theme.simpleEnrollment` をカスタムテーマで置き換えます。
* /etc/designs/mycompany の下に新しいクライアントライブラリを定義します。JSP ページで、デフォルトのテーマのエントリの後にクライアントライブラリを含めます。このクライアントライブラリに、上書きされたすべてのスタイルと追加のJava Scriptファイルを含めます。

>[!NOTE]
>
>アダプティブフォームのレンダリングに使用されるページコンポーネントに含まれるクライアントライブラリが、テーマによって参照されます。クライアントライブラリは、主にアダプティブフォームの外観を管理します。

