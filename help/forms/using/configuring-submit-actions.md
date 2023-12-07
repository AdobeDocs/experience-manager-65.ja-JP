---
title: 送信アクションの設定
description: Formsでは、送信アクションを設定して、送信後のアダプティブフォームの処理方法を定義することができます。 組み込みの送信アクションを使用することも、独自のアクションを一から書き込むこともできます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 85%

---

# 送信アクションの設定 {#configuring-the-submit-action}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | この記事 |


## 送信アクションの概要 {#introduction-to-submit-actions}

送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームで送信アクションを設定することができます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか用意されています。 デフォルトの送信アクションをコピーし、拡張することにより、独自の送信アクションを作成できます。ただし、要件に応じて、送信したフォームのデータを処理する独自の送信アクションを書いて登録できます。送信アクションは、[同期または非同期の送信](../../forms/using/asynchronous-submissions-adaptive-forms.md)を使用できます。

サイドバーにある「アダプティブフォームコンテナ」プロパティの「**送信**」セクションで、送信アクションを設定できます。

![送信アクションの設定](assets/thank-you-setting.png)

送信アクションの設定

アダプティブフォームで使用できるデフォルトの送信アクションは次のとおりです。

* REST エンドポイントへの送信
* メールを送信
* 電子メールでPDFを送信
* Forms ワークフローを起動
* フォームデータモデルを使用して送信
* フォームポータル送信アクション
* AEM ワークフローを起動
* Power Automate に送信

>[!NOTE]
>
>メールで PDF を送信アクションは、XFA テンプレートをフォームモデルとして使用しているアダプティブフォームにのみ使用できます。

>[!NOTE]
>
>[AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM フォルダー
>が存在することを確認します。ディレクトリは、添付ファイルを一時的に保存するために必要になります。ディレクトリが存在しない場合は作成します。

>[!CAUTION]
>
>フォームテンプレート、フォームデータモデル、スキーマベースのアダプティブフォームのいずれかを、スキーマ（XML スキーマ、JSON スキーマ、フォームテンプレート、フォームデータモデルのいずれか）に準拠した XML データや JSON データを使用して[事前入力](../../forms/using/prepopulate-adaptive-form-fields.md)する、つまりデータが &lt;afData>、&lt;afBoundData>、&lt;/afUnboundData> のタグを含まない場合、アダプティブフォームの連結されていないフィールド（連結されていないフィールドとは、[bindref](../../forms/using/prepopulate-adaptive-form-fields.md) プロパティのないアダプティブフォームフィールドのこと）のデータは失われます。

アダプティブフォームがユースケースを実現するように、カスタム送信アクションを作成できます。詳しくは、「[アダプティブフォーム向けのカスタム送信アクションの作成](../../forms/using/custom-submit-action-form.md)」を参照してください。

## REST エンドポイントへの送信 {#submit-to-rest-endpoint}

The **REST エンドポイントに送信** 送信オプションでは、フォームに入力されたデータを HTTP データリクエストの一環として設定済みの確認ページにGETを渡します。 リクエストにフィールド名を追加できます。リクエストのフォーマットを以下に示します。

`{fieldName}={request parameter name}`

以下の画像に示すとおり、`param1` と `param2` が、**textbox** フィールドと **numericbox** フィールドからコピーした値を持つパラメーターとして次のアクションに向けて渡されます。

また、**POST リクエストを有効にする**&#x200B;ことで、リクエストを投稿するための URL を指定することもできます。フォームをホストする Experience Manager サーバーにデータを送信するには、Experience Manager サーバーのルートパスに対応する相対パスを使用します。例：/content/forms/af/SampleForm.html 他のサーバーにデータを送信するには、絶対パスを使用します。

![REST エンドポイント送信アクションの設定](assets/action-config.png)

REST エンドポイント送信アクションの設定

>[!NOTE]
>
フィールドを REST URL 内のパラメーターとして渡すには、すべてのフィールドが異なる要素名を持っている必要があります。これは、異なるパネルに置かれているフィールドにも適用されます。

### 送信されたデータをリソースまたは外部の REST エンドポイントに投稿  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

**REST エンドポイントへの送信**&#x200B;アクションを使用して、送信されたデータを REST URL に POST できます。URL は、内部（フォームがレンダリングされるサーバー）または外部サーバーのどちらのものでも使用できます。

内部サーバーにデータを POST 送信するには、リソースのパスを指定します。データは、リソースのパスに POST されます。例えば、/content/restEndPoint です。このような POST リクエストには、送信リクエストの認証情報が使用されます。

外部サーバーにデータを POST 送信するには、URL を指定します。URL の形式は、https://host:port/path_to_rest_end_point です。POST リクエストを匿名で処理するためのパスを設定してください。

![「ありがとうございます」ページのパラメーターとして渡されたフィールド値のマッピング](assets/post-enabled-actionconfig.png)

上の例で、ユーザーが `textbox` に入力した情報は、パラメーター `param1` を使用して取得されます。`param1` を使用して取得されるデータを POST するための構文を以下に示します。

`String data=request.getParameter("param1");`

同様に、XML データと添付ファイルの POST に使用するパラメーターは、`dataXml` および `attachments` です。

例えば、この 2 つのパラメーターをスクリプト中で使用して、REST エンドポイントに送信されたデータを解析できます。データを格納および解析するための構文を以下に示します。

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

この例では、`data` が XML データを格納し、`att` が添付ファイルデータを格納します。

## メールを送信 {#send-email}

「**メールを送信**」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にメールが送信されます。生成されるメールには、事前に定義された形式のフォームデータを含めることができます。

>[!NOTE]
>
フォームデータを電子メールに含めるには、異なるパネルに配置されている場合でも、すべてのフォームフィールドに異なる要素名を付ける必要があります。

## 電子メールでPDFを送信 {#send-pdf-via-email}

「**メールで PDF を送信**」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にフォームデータを含む PDF が添付されたメールが送信されます。

>[!NOTE]
>
この送信アクションは、レコードのドキュメントテンプレートを持つ XFA ベースのアダプティブフォームと XSD ベースのアダプティブフォームに使用できます。

## Forms ワークフローを起動 {#invoke-a-forms-workflow}

「**Forms Workflow への送信**」送信オプションでは、データ XML および添付ファイル（存在する場合に）が既存の Adobe LiveCycle プロセスまたは JEE での AEM Forms プロセスに送信されます。

送信アクション「Forms Workflow への送信」の設定方法について詳しくは、「[フォームワークフローを使用したフォームデータの送信および処理](../../forms/using/submit-form-data-livecycle-process.md)」参照してください。

## フォームデータモデルを使用して送信 {#submit-using-form-data-model}

「**フォームデータモデルを使用して送信**」送信アクションでは、フォームデータモデルの特定のデータモデルオブジェクトで送信したアダプティブフォームデータをデータソースに書き込みます。送信アクションを設定する際に、データソースに書き戻す送信済みデータを持つデータモデルオブジェクトを選択できます。

さらに、フォームデータモデルとレコードのドキュメント (DoR) を使用して、フォームの添付ファイルをデータソースに送信できます。

フォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

## フォームポータル送信アクション {#forms-portal-submit-action}

「**フォームポータル送信アクション**」オプションでは、フォームデータが AEM Forms ポータルで使用できるようになります。

Forms Portal と送信アクションについて詳しくは、 [ドラフトと送信コンポーネント](../../forms/using/draft-submission-component.md).

## AEM ワークフローを起動 {#invoke-an-aem-workflow}

「**[!UICONTROL AEM ワークフローを起動]**」送信アクションは、アダプティブフォームを [AEM ワークフロー](/help/sites-developing/workflows-models.md)と関連付けます。フォームが送信されると、関連するワークフローがオーサーインスタンスで自動的に起動します。データファイル、添付ファイル、レコードのドキュメントは、相対するフォルダーや、ワークフローのペイロードの場所または変数に保存できます。ワークフローが外部データストレージ用にマークされている場合、ペイロードオプションではなく変数オプションが使用可能になります。ワークフローモデルで使用できる変数のリストから選択できます。ワークフローの作成時ではなく、後の段階で外部データストレージの対象としてワークフローがマークされている場合は、必要な変数設定が適切に行われていることを確認します。

「**AEM ワークフローを起動**」送信アクションを使用する前に、[Experience Manager DS の設定を行います](../../forms/using/configuring-the-processing-server-url-.md)。AEM ワークフローの作成について詳しくは、「[OSGi 上の Forms 中心のワークフロー](../../forms/using/aem-forms-workflow.md)」を参照してください。

送信アクションは、ワークフローのペイロードの場所に以下を配置します。ただし、ワークフローモデルが外部データストレージ用にマークされている場合は「変数」オプションのみが表示され、ペイロードオプションは表示されないことに注意してください。

* **データファイル**：アダプティブフォームに送信されたデータを含みます。「**[!UICONTROL データファイルパス]**」オプションを使用して、ファイル名とペイロードを基準とするファイルのパスを指定できます。例えば、`/addresschange/data.xml` パスは、`addresschange` という名前のフォルダーを作成し、ペイロードを基準に配置します。フォルダー階層を作成せずに、`data.xml` のみを指定して、送信されたデータのみを送信することもできます。「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

>[!NOTE]
>
変数は、ワークフローモデルが外部データストレージ用にマークされているかどうかに関係なく使用できます。

* **添付ファイル**：「**[!UICONTROL 添付ファイルのパス]**」オプションを使用して、アダプティブフォームにアップロードされた添付ファイルの保存先となるフォルダー名を指定できます。フォルダーがペイロードを基準に作成されます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

* **レコードのドキュメント**：アダプティブフォーム用に生成されたレコードのドキュメントを含みます。「**[!UICONTROL レコードのドキュメントパス]**」オプションを使用して、レコードのドキュメントファイル名と、ペイロードを基準にファイルのパスを指定できます。例えば、`/addresschange/DoR.pdf` パスは、ペイロードを基準に `addresschange` という名前のフォルダーを作成し、ペイロードを基準に `DoR.pdf` を配置します。`DoR.pdf` のみを指定して、フォルダー階層を作成せずに、レコードのドキュメントのみを保存することもできます。ワークフローが外部データストレージ用にマークされている場合は、「変数」オプションを使用し、ワークフローモデルで使用可能な変数のリストから変数を選択します。

## Power Automate に送信 {#microsoft-power-automate}

送信時に Microsoft® Power Automate のクラウドフローを実行するように、アダプティブフォームを設定できます。設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate クラウドフローに送信して処理します。 Microsoft® Power Automate の機能を活用して、キャプチャされたデータを中心にビジネスロジックを構築し、顧客のワークフローを自動化しながら、カスタムのデータキャプチャエクスペリエンスを構築するのに役立ちます。アダプティブフォームを Microsoft® Power Automated と統合した後に実行できる操作の例を以下に示します。

* Power Automate のビジネスプロセスでアダプティブフォームデータを使用する
* Power Automate を使用して、500 を超えるデータソースまたは一般公開されている API にキャプチャしたデータを送信する
* キャプチャしたデータに対する複雑な計算を実行する
* 事前に定義されたスケジュールでアダプティブフォームのデータをストレージシステムに保存する

アダプティブフォームエディターには「**Microsoft Power Automate フローの呼び出し**」送信アクションが用意されており、アダプティブフォームのデータ、添付ファイル、レコードのドキュメントを Power Automate クラウドフローに送信することができます。送信アクションを使用して、取得したデータをMicrosoft® Power Automate に送信するには、次の手順を実行します。 [AEM FormsインスタンスをMicrosoft® Power Automate に接続する](/help/forms/using/forms-microsoft-power-automate-integration.md)

「[Microsoft® Power Automate フローの呼び出し](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action)」送信アクションを使用して、Power Automate フローにデータを送信する

## アダプティブフォームにおけるサーバー側の再検証 {#server-side-revalidation-in-adaptive-form}

通常、どのようなオンラインデータ取得システムでも、ビジネスルールを適用するために、開発者はクライアントサイドに何らかの JavaScript 検証を配置します。しかし、最新のブラウザーでは、エンドユーザーが Web Browser DevTools Console などの様々な手法を使用してこれらの検証を回避し、手動で送信を行える方法が存在します。このような手法は、アダプティブフォームにも有効です。フォーム開発者は、多様な検証ロジックを作成できますが、エンドユーザーは、これらの検証ロジックを回避し、無効なデータをサーバーに送信できます。無効なデータは、フォーム作成者が適用したビジネスルールを破ることになります。

サーバー側の再検証機能を使用すると、アダプティブフォームの作成者がサーバー上でアダプティブフォームをデザインする際に指定した検証を実行することもできます。 これは、フォームの検証で表されるデータ送信の漏洩やビジネスルール違反の可能性を阻止します。

### サーバー側で検証されるもの  {#what-to-validate-on-server-br}

アダプティブフォームの追加設定なし（OOTB）のフィールド検証で、サーバーで再実行されるものは次のとおりです。

* 必須
* 検証パターン形式文字列
* 検証式

### サーバー側検証の有効化 {#enabling-server-side-validation-br}

サイドバーにある「アダプティブフォームコンテナ」の「**サーバー側で再検証**」を使用して、現在のフォームのサーバーサイド検証を有効または無効にします。

![サーバーサイド検証の有効化](assets/revalidate-on-server.png)

サーバーサイド検証の有効化

エンドユーザーがこれらの検証を回避してフォームを送信した場合、サーバーが再度検証を行います。サーバーサイドでの検証が失敗した場合、送信処理が中止されます。エンドユーザーには、元のフォームが再度表示されます。取得されたデータおよび送信されたデータは、エラーとしてユーザーに表示されます。

>[!NOTE]
>
サーバーサイド検証により、フォームモデルが検証されます。検証用に別個のクライアントライブラリを作成し、同じクライアントライブラリ内でHTMLのスタイル設定や DOM 操作など他の要素と混在させないことをお勧めします。

### 検証式でのカスタム関数のサポート {#supporting-custom-functions-in-validation-expressions-br}

複雑な検証ルールがある場合、正確な検証スクリプトがカスタム関数の中に存在し、作成者がこれらのカスタム関数をフィールド検証式から呼び出すことがあります。このカスタム関数ライブラリをサーバーサイド検証中に認識させ、利用可能にするために、フォーム作成者は、「アダプティブフォームコンテナ」プロパティの「**基本**」タブで、AEM クライアントライブラリの名前を設定できます（下記画像を参照）。

![検証式でのカスタム関数のサポート](assets/clientlib-cat.png)

検証式でのカスタム関数のサポート

作成者は、アダプティブフォームごとにカスタム JavaScript ライブラリを設定できます。ライブラリには、jQuery および underscore.js サードパーティライブラリに依存する、再利用可能な関数のみを保持します。

## 送信アクションに対するエラー処理 {#error-handling-on-submit-action}

Experience Manager セキュリティおよび堅牢化ガイドラインの一部として、404.jsp や 500.jsp などのカスタムエラーページを設定してください。これらのハンドラーは、フォームの送信時に 404 エラーまたは 500 エラーが表示されるときに呼び出されます。 また、これらのハンドラーは、パブリッシュノードでこれらのエラーコードがトリガーされるときにも呼び出されます。

詳しくは、「[エラーハンドラーによって表示されるページのカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md)」を参照してください。
