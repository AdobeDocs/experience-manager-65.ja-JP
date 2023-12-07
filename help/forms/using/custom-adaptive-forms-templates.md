---
title: カスタムアダプティブフォームのテンプレートの作成
description: この記事では、カスタムアダプティブフォームテンプレートの作成方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 65%

---

# カスタムアダプティブフォームのテンプレートの作成{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Formsでは、動的テンプレートが導入されました。 AEM Sitesテンプレートエディターを使用して、 [動的テンプレートの作成または編集](../../forms/using/template-editor.md). この記事で説明するテンプレートは、静的テンプレートです。 これらは、デフォルトのインストールでは使用できません。 [互換性パッケージをインストール](../../forms/using/compatibility-package.md)すると、静的なテンプレートを入手することができます。 

## 前提条件 {#prerequisites}

* AEM [ページテンプレート](/help/sites-authoring/templates.md)および[アダプティブフォームオーサリング](https://helpx.adobe.com/jp/aem-forms/6-1/introduction-forms-authoring.html)に関する知識

* AEMについて [クライアント側ライブラリ](/help/sites-developing/clientlibs.md)

## アダプティブフォームテンプレート {#adaptive-form-template}

アダプティブフォームテンプレートは、アダプティブフォームの作成に使用される特定のプロパティとコンテンツ構造を持つ特殊な AEM ページテンプレートです。このテンプレートには、レイアウト、スタイルおよび基本的な初期コンテンツ構造が事前に設定されています。

フォームを作成すると、オリジナルテンプレートのコンテンツ構造が変更された場合でも、フォームには反映されません。

## デフォルトのアダプティブフォームテンプレート {#default-adaptive-form-templates}

AEM QuickStart は、次のアダプティブフォームテンプレートを提供します。

* サーベイのテンプレート：複数の列が設定されたレスポンシブレイアウトを使用して単一ページのアダプティブフォームを作成します。フォームを表示させる画面サイズに基づいてレイアウトは自動で調整されます。
* 登録テンプレート：ウィザードのレイアウトを使用して複数の手順を備えたアダプティブフォームを作成します。このレイアウトでは、各手順の完了に必要な式を指定できます。指定した式は、次の手順にウィザードを進める前に検証されます。
* タブ付き登録テンプレート：タブが左側にあるレイアウトを使用し、複数のタブを備えたアダプティブフォームを作成します。このレイアウトでは、任意の順序でタブにアクセスできます。
* 高度な登録テンプレート：複数のタブとウィザードを含むフォームを作成できます。 タブが左側にあるレイアウトを使用して、任意の順序でタブにアクセスできます。 署名と検証には Adobe Document Cloud eSign サービスを使用します。
* 空のテンプレート：ヘッダー、フッター、初期コンテンツを含まないフォームを作成できます。 テキストボックス、ボタン、画像などのコンポーネントを追加できます。 空白テンプレートでは、[AEM サイトページに埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md)ことができるフォームを作成します。

これらのテンプレートでは、`sling:resourceType` プロパティが、対応するページのコンポーネントに設定されています。ページコンポーネントは、アダプティブフォームコンテナを含む CQ ページをレンダリングし、アダプティブフォームをレンダリングします。

次の表は、テンプレートとページコンポーネントの間の関連を列挙します。

<table>
 <tbody>
  <tr>
   <td><p><strong>テンプレート</strong></p> </td>
   <td><p><strong>ページコンポーネント </strong></p> </td>
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

テンプレートエディターを使用して、アダプティブフォームの構造と初期コンテンツを指定できます。例えば、すべてのフォーム作成者が、登録フォーム内にテキストボックス、ナビゲーションボタン、送信ボタンをいくつか持つようにします。 作成者が他の登録フォームと一貫性のあるフォームを作成できるテンプレートを作成できます。 AEM Template Editor では、次のことが可能です。

* 構造レイヤーにフォームのヘッダーおよびフッターコンポーネントを追加する
* フォームの初期コンテンツを提供できます。
* テーマを指定できます。
* 送信、リセット、移動などの操作を指定できます。

詳しくは、[テンプレートエディター](../../forms/using/template-editor.md)を参照してください。

## CRXDE からのアダプティブフォームテンプレートの作成 {#creating-an-adaptive-form-template-from-crxde}

使用可能なテンプレートを使用する代わりに、テンプレートを作成してアダプティブフォームを作成することができます。 カスタムテンプレートは、アダプティブフォームのコンテナやページ要素（ヘッダーやフッターなど）を参照する様々なページコンポーネントに基づいています。

これらのコンポーネントは Web サイト向けの基本ページコンポーネントを使用して作成することができます。または、あらかじめ用意されたテンプレートで使用されるアダプティブフォームのページコンポーネントを拡張することもできます。

simpleEnrollmentTemplate などのカスタムテンプレートを作成するには、次の手順を実行します。

1. オーサーインスタンスで CRXDE Lite に移動します。

1. /apps ディレクトリの下に、アプリケーションのフォルダー構造を作成します。 例えば、アプリケーション名が mycompany の場合は、この名前のフォルダーを作成します。 通常、アプリケーションフォルダーには、components、configuration、templates、src および installation ディレクトリが含まれます。 この例では、components、configuration、templates の各フォルダーを作成します。

1. /libs/fd/af/templates フォルダーに移動します。
1. `simpleEnrollmentTemplate` ノードをコピーします。
1. /apps/mycompany/templates フォルダーに移動します。 右クリックし、「 」を選択します。 **[!UICONTROL 貼り付け]**.
1. 必要に応じて、コピーしたテンプレートノードの名前を変更します。 例えば、enrollment-template などに変更します。

1. /apps/mycompany/templates/enrollment-template に移動します。

1. `jcr:content` ノードの `jcr:title` プロパティと `jcr:description` プロパティを変更し、コピー元のテンプレートと区別できるようにします。

1. 変更したテンプレートの `jcr:content` ノードには、`guideContainer` と `guideformtitle` のコンポーネントが含まれます。`guideContainer` はアダプティブフォームを格納するコンテナです。`guideformtitle` コンポーネントは、アプリケーション名や説明などを表示します。

   `guideformtitle` の代わりに、カスタムコンポーネントまたは `parsys` コンポーネントを含めることができます。例えば、`guideformtitle` を削除して、カスタムコンポーネントまたは `parsys` コンポーネントのノードを含めることができます。コンポーネントの `sling:resourceType` プロパティの参照先が、そのコンポーネントになっていることを確認してください。ページ `component.jsp` ファイルでも同様に定義されます。

1. /apps/mycompany/templates/enrollment-template/jcr:content に移動します。

1. 「**[!UICONTROL プロパティ]**」タブを開き、`cq:designPath` プロパティの値を /etc/designs/mycompany に変更します。

1. 次に、`cq:Page` タイプに /etc/designs/mycompany のノードを作成します。

## アダプティブフォームのページコンポーネントを作成する {#create-an-adaptive-form-page-component}

テンプレートはページコンポーネント/libs/fd/af/components/page/base を参照するので、カスタムテンプレートはデフォルトテンプレートと同じスタイルを持ちます。 コンポーネントの参照は、/apps/mycompany/templates/enrollment-template/jcr:content ノードで定義された `sling:resourceType` プロパティで検索できます。ベースはコア製品のコンポーネントのため、変更を加えないでください。

1. /apps/mycompany/templates/enrollment-template/jcr:content のノードに移動し、`sling:resourceType` プロパティの値を /apps/mycompany/components/page/enrollmentpage に変更します。
1. /libs/fd/af/components/page/base のノードを /apps/mycompany/components/page フォルダーにコピーします。

1. コピーしたコンポーネントの名前を `enrollmentpage` に変更します。

1. **（コンテンツページをすでに持っている場合に限ります）** 自分の web サイトに `contentpage` コンポーネントがすでに存在する場合、次の手順（a-d）を実行します。自分の Web サイトに `contentpage` コンポーネントが存在しない場合は、`resourceSuperType` プロパティを OOTB の基本ページにポイントしたままにすることができます。

   1. `enrollmentpage` ノードの場合、`sling:resourceSuperType` プロパティの値を mycompany/components/page/contentpage に設定します。`contentpage` コンポーネントは、自分のサイトの基本ページコンポーネントです。他のページコンポーネントで拡張することができます。`enrollmentpage` の下で、`head.jsp`、`content.jsp`、`library.jsp` を除くスクリプトファイルを削除します。このケースでは `contentpage` である `sling:resourceSuperType` コンポーネントに、このようなスクリプトすべてが含まれます。ナビゲーションバーやフッターなどを含むヘッダー類は、`contentpage` コンポーネントから継承されます。

   1. `head.jsp` ファイルを開きます。

      この JSP ファイルには `<cq.include script="library.jsp"/>` 行が含まれます。

      `library.jsp` ファイルには、`guide.theme.simpleEnrollment` のクライアントライブラリが含まれ、その中にアダプティブフォームのスタイル設定が含まれています。

      `enrollmentpage` のページコンポーネントは専用の `head.jsp` ファイルがあり、`contentpage` コンポーネントの `head.jsp` ファイルをオーバーライドします。

   1. `enrollmentpage` コンポーネント用の `head.jsp` ファイルに、`contentpage` コンポーネント用の `head.jsp` ファイルのすべてのスクリプトを含めます。
   1. `content.jsp` スクリプトの中に、追加のページコンテンツまたはページがレンダリングされる際に含まれる他のコンポーネントへの参照を追加することができます。例えば、`applicationformheader` カスタムコンポーネントを追加する場合、JSP ファイルのコンポーネントに次の参照を追加します。

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同様に、テンプレートのノード構造に `parsys` コンポーネントを追加する場合、カスタムコンポーネントも含めます。

## アダプティブフォームのクライアントライブラリの作成 {#creating-an-adaptive-form-client-library}

新しいテンプレート用の `enrollmentpage` コンポーネントの `head.jsp` ファイルには、`guide.theme.simpleEnrollment` クライアントライブラリが含まれます。デフォルトのテンプレートも、このクライアントライブラリを使用します。 次のいずれかの方法を使用して、新しいテンプレートのスタイルを変更します。

* カスタムテーマを定義し、デフォルトのテーマ `guide.theme.simpleEnrollment` をカスタムテーマで置き換えます。
* /etc/designs/mycompany の下に新しいクライアントライブラリを定義します。 JSP ページのデフォルトのテーマエントリの後にクライアントライブラリを含めます。 このクライアントライブラリに、オーバーライドされたすべてのスタイルと、追加の Java Script ファイルを含めます。

>[!NOTE]
>
>アダプティブフォームのレンダリングに使用されるページコンポーネントに含まれるクライアントライブラリが、テーマによって参照されます。クライアントライブラリは、主にアダプティブフォームの外観を管理します。
