---
title: アダプティブフォームのテーマを作成またはカスタマイズする方法は？
seo-title: How to create a theme for Adaptive Forms Core Components?
description: BEM 仕様を使用して、アダプティブFormsコアコンポーネントのテーマを作成またはカスタマイズする方法を説明します。
seo-description: Learn to create or customize themes for Adaptive Forms Core Components using BEM specifications
keywords: アダプティブフォームのコアコンポーネントテーマの作成、新しいテーマの作成、テーマのカスタマイズ、新しいテーマのアップロード、フォームでのテーマの使用、テーマの削除、AEM 6.5 forms でのテーマの作成
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 1b97dc536550da8904bc7da09e983e0722c42a3d
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 9%

---


# アダプティブフォームテーマの作成またはカスタマイズ {#introduction-to-theme}

<span class="preview"> Adobeでは、コアコンポーネントを次のように使用することをお勧めします。 [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) または [スタンドアロンのアダプティブFormsを作成](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | この記事 |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |

**適用先：** ✅アダプティブフォームのコアコンポーネント❎ [アダプティブフォームの基盤コンポーネント](/help/forms/using/themes.md).

AEM Forms 6.5 では、テーマは、アダプティブフォームのスタイル（ルックアンドフィール）を定義するために使用するAEMクライアントライブラリです。 テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマは、アダプティブフォームを参照せずに独立して管理され、複数のアダプティブFormsで再利用できます。

## 使用可能なテーマ {#available-standard-theme}

AEM 6.5 環境は、コアコンポーネントベースのアダプティブForms向けに、次のテーマを提供しています。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

## テーマの構造について {#understanding-structure-of-theme}

テーマは、CSS ファイル、JavaScript ファイル、およびアダプティブFormsのスタイルを定義するリソース（アイコンなど）を含むパッケージです。 アダプティブフォームテーマは、次のコンポーネントで構成される特定の組織に従います。

* `src/theme.scss`:このフォルダーには、テーマ全体に大きな影響を与える CSS ファイルが含まれています。 テーマのスタイル設定と動作を一元的に定義および管理できます。 このファイルを編集すると、テーマ全体で共通に適用される変更を加え、アダプティブFormsとAEM Sitesの両方のページの外観と機能に影響を与えることができます。

* `src/site`:このフォルダーには、AEMサイトのページ全体に適用される CSS ファイルが含まれます。 これらのファイルは、AEM Site のページの全体的な機能やレイアウトに影響を与えるコードとスタイルで構成されています。 ここで行った変更は、サイトのすべてのページに反映されます。

* `src/components`:このフォルダーの CSS ファイルは、AEMの個々のコアコンポーネント用に設計されています。 コンポーネント用の各専用フォルダーには、 `.scss` アダプティブフォーム内の特定のコンポーネントのスタイルを設定するファイル 例えば、 `/src/components/button/_button.scss` ファイルには、アダプティブFormsボタンコンポーネントのスタイル情報が含まれています。

  ![キャンバステーマの構造](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`:このフォルダーには、アイコン、ロゴ、フォントなどの静的ファイルが含まれます。 これらのリソースは、テーマの視覚的要素と全体的なデザインを強化するために使用されます。

## テーマの作成

AEM Forms 6.5 では、コアコンポーネントベースのアダプティブFormsの標準テーマを以下に示します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

以下が可能です。 [これらの標準のテーマをカスタマイズしてテーマを作成する](#customize-a-theme-core-components).

## テーマのカスタマイズ {#customize-a-theme-core-components-based-adaptive-forms}

テーマのカスタマイズとは、テーマの外観を変更し、パーソナライズするプロセスを指します。 テーマをカスタマイズすると、デザイン要素、レイアウト、色、タイポグラフィ、および基になるコードに変更を加えることができます。 これにより、テーマで提供される基本的な構造と機能を維持しながら、Web サイトやアプリケーションの独自のカスタマイズされた外観を作成できます。

>[!NOTE]
>
> * パッケージマネージャーを使用して、すべてのオーサーインスタンスとパブリッシュインスタンスにテーマをデプロイします。
> * テーマのクライアントライブラリは、他のパッケージと同様に、パッケージマネージャーを使用してインポートまたはエクスポートされます。

### テーマをカスタマイズするための前提条件 {#prerequisites}

* [アダプティブFormsコアコンポーネントの有効化](/help/forms/using/enable-adaptive-forms-core-components.md) 環境に適用されます。

* 最新リリースのをインストールする [Apache Maven。](https://maven.apache.org/download.cgi) Apache Maven は、Java™プロジェクトで一般的に使用されるビルド自動化ツールです。 最新のリリースをインストールすると、テーマのカスタマイズに必要な依存関係が確保されます。

* を作成する方法を学ぶ [Adobe Experience Managerのクライアントライブラリ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=ja). AEMはクライアントライブラリを提供します。このライブラリを使用すると、クライアントサイドコードをリポジトリに保存し、カテゴリに整理し、コードの各カテゴリをクライアントに提供するタイミングと方法を定義できます。

* プレーンテキストエディターをインストールします。 例： Microsoft® Visual Studio Code。 Microsoft® Visual Studio Code などのプレーンテキストエディターを使用すると、テーマファイルの編集と変更を行う際に使いやすい環境を提供します。

* AEM Forms環境が起動および実行中であることを確認します。

### テーマをカスタマイズする際の考慮事項 {#consideration}

* 必ず [アダプティブFormsコアコンポーネントの有効化に使用するアーキタイププロジェクト](/help/forms/using/enable-adaptive-forms-core-components.md) を使用してテーマをカスタマイズします。

* アダプティブフォームを公開する際、クライアントライブラリはパブリッシュインスタンスで自動的には公開されません。 必ず、アダプティブフォーム内で参照されているクライアントライブラリをパブリッシュ環境に手動で公開してください。

* Adobeは、クライアントライブラリのクラス名を変更しないことをお勧めします。

### テーマのカスタマイズ {#customize-a-theme-core-components}

テーマの作成またはカスタマイズは、複数の手順で行います。 テーマを作成/カスタマイズするには、次の手順をリストに示す順序で実行します。

1. [標準テーマの複製](#clone-git-repo-of-theme)
1. [テーマの外観のカスタマイズ](#customize-the-theme)
1. [ローカルデプロイメント用のテーマの準備](#generate-the-clientlib)
1. [テーマをローカル環境にデプロイする](#deploy-the-theme-on-a-local-environment)
1. [テーマを実稼動環境にデプロイする](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

このドキュメントで示す例は、 **キャンバス** テーマを作成する場合は、任意の標準テーマを複製し、同じ手順を使用してカスタマイズできます。 これらの手順はどのテーマにも適用でき、特定のニーズに応じてテーマを変更できます。

#### 1.テーマの Git リポジトリを複製します。 {#clone-git-repo-of-theme}

コアコンポーネントベースのアダプティブFormsの標準テーマを複製するには、次の標準テーマのいずれかを選択します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL のテーマ](https://github.com/adobe/aem-forms-theme-easel)

標準のテーマを複製するには、次の手順を実行します。

1. コマンドプロンプトまたはターミナルウィンドウをローカル開発環境で開きます。

1. を実行します。 `git clone` コマンドを使用してテーマを複製します。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   を [テーマの Git リポジトリのパス] を、テーマの対応する Git リポジトリの実際の URL に置き換えます。

   たとえば、キャンバステーマを複製するには、次のコマンドを実行します。

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. 「**親フォルダー内のすべてのファイルの作成者を信頼する**」を選択し、「**はい、私は作成者を信頼します**」をクリックします。

コマンドを正常に実行すると、そのテーマのローカルコピーが  `aem-forms-theme-canvas` フォルダー。

#### 2. テーマをカスタマイズする {#customize-the-theme}

個々のコンポーネントをカスタマイズしたり、テーマのグローバル変数を使用してテーマレベルの変更を行う柔軟性があります。 グローバル変数を変更すると、個々のコンポーネントすべてにカスケード効果が適用されます。 例えば、グローバル変数を利用して、アダプティブフォーム内のすべてのコンポーネントの境界線の色を変更したり、活発な塗りの色をコールトゥアクション (CTA) ボタンに適用したりできます。 以下の操作を実行できます。

* [テーマレベルのスタイルを設定する](#theme-customization-global-level)

* [コンポーネントレベルスタイルを設定](#component-based-customization)

##### テーマレベルのスタイルを設定する {#theme-customization-global-level}

この `variable.scss` ファイルには、テーマのグローバル変数が含まれます。 これらの変数を更新すると、テーマレベルでスタイル関連の変更を行うことができます。 テーマレベルのスタイルを適用するには、次の手順に従います。

1. `<your-theme-sources>/src/site/_variables.scss` ファイルを編集用に開きます。
1. プロパティの値を変更します。 例えば、デフォルトのエラー色は赤です。 エラーの色を赤から青に変更するには、 `$error`変数を使用します。 例：`$error: #196ee5`

   ![例：エラーの色が青に設定されました](/help/forms/using/assets/theme-level-changes.png)

1. ファイルを保存して閉じます。


同様に、 `variable.scss` ファイル：複数のアダプティブフォームコンポーネントに影響を与えるフォントファミリーと種類、テーマとフォントの色、フォントサイズ、テーマの間隔、エラーアイコン、テーマの境界線のスタイル、その他の変数を設定します。

##### コンポーネントレベルスタイルを設定 {#component-based-customization}

また、特定のアダプティブフォームコアコンポーネント（ボタン、チェックボックス、コンテナ、フッターなど）のフォント、色、サイズおよびその他の CSS プロパティをカスタマイズすることもできます。 特定のコンポーネントに関連付けられた CSS ファイルを編集することで、そのスタイルを組織のブランディングに合わせることができます。 コンポーネントのスタイルをカスタマイズするには、次の手順に従います。

1. ファイルを開きます。 `<your-theme-sources>/src/components/<component>/<component.scss>` （編集用） 例えば、ボタンコンポーネントのフォントカラーを変更するには、 `<your-theme-sources>/src/components/button/button.scss`、ファイル。
1. 必要に応じて、の値を変更します。 例えば、マウスポインターを置いたときのボタンコンポーネントの色を緑に変更するには、 `color: $white` プロパティを `cmp-adaptiveform-button__widget:hover` 16 進コード#12b453またはその他の緑のシェードへのクラス。 最終的なコードは次のようになります。

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. ファイルを保存して閉じます。

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>
>
> テーマレベルとコンポーネントレベルの両方でスタイルを定義する場合、コンポーネントレベルで定義されたスタイルが優先されます。


#### 3.テーマをデプロイする準備をする {#generate-the-clientlib}

テーマをAEMインスタンスにデプロイするには、テーマをクライアントライブラリに変換する必要があります。 テーマをクライアントライブラリに変換するには、次の手順に従います。

1. コマンドプロンプトまたはターミナルウィンドウを開きます。
1. `<your-theme-sources>` フォルダーに移動します。例：`C:\aem-forms-theme-canvas`
1. 次のコマンドを実行します。

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   置換 `[yourtheme]` をカスタムテーマの名前に置き換えます。 例えば、カスタムテーマの名前が `customcanvastheme`、次のコマンドを実行します。

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   コマンドが正常に実行されると、クライアントライブラリフォルダーが `themerepo\theme-clientlibs\[yourtheme]`.

   ![クライアントライブラリの生成](/help/forms/using/assets/clientlib_created.png)


   ![クライアントライブラリの場所](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4.テーマをローカル環境にデプロイする {#deploy-the-theme-on-a-local-environment}

テーマをローカル開発またはテスト環境にデプロイするには、次の手順に従います。

1. 前の節で作成したクライアントライブラリを、アーキタイププロジェクトの次のパスにコピーします。

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. コマンドプロンプトまたはターミナルを開きます。
1. アダプティブフォームのコアコンポーネントを有効にするために使用するプロジェクトである、AEM Archetype プロジェクトのルートディレクトリに移動します。
1. 次のコマンドを実行して、環境にカスタムテーマをデプロイします。

   `mvn clean install`

   ![クライアントライブラリビルド](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5.実稼動環境にテーマをデプロイする {#deploy-theme}

ローカル開発環境でテーマを正常にテストしたら、作成者インスタンスと発行インスタンスの両方を含む実稼動環境にテーマをデプロイする手順に進むことができます。 テーマを実稼動環境にデプロイするには、次の手順に従います。

1. AEM環境にログインします。
1. パッケージマネージャーを開きます。 デフォルトの URL は `https://localhost:4502/crx/packmgr/index.jsp` です。
1. クリック **パッケージをアップロード** をクリックし、 **参照**.
1. に移動して選択します。 `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. クリック **開く**.
1. 「インストール」をクリックします。すべての実稼動環境でこの手順を繰り返します。


パッケージがインストールされると、テーマを選択できるようになります。

![テーマクライアントライブラリ](/help/forms/using/assets/themeclientlibrary.png)

>
>
>パブリッシュインスタンスのログインダイアログにアクセスして、パッケージマネージャーを通じてパッケージをインストールできない場合は、次の URL からログインしてみてください。 `http://[Publish Server URL]:[PORT]/system/console`. これにより、パブリッシュインスタンスにログインする権限が与えられ、インストールプロセスに進むことができます。

## テーマをアダプティブフォームに適用する {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用する手順は次のとおりです。

1. ローカルのAEMオーサーインスタンスにログインします。
1. Experience Manager のログインページに資格情報を入力します。**Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;の順にタップします。
1. **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。
1. アダプティブFormsコアコンポーネントテンプレートを選択し、 **次へ**. この **プロパティを追加** 表示
1. 次を指定： **名前** アダプティブフォームの

   >[!NOTE]
   >
   > * デフォルトでは、 `adaptiveform.theme.canvas3` テーマが選択されている。
   > * 別のテーマを **テーマクライアントライブラリ** ドロップダウンメニュー。

1. 「**作成**」をクリックします。

アダプティブフォームのテーマは、アダプティブフォームの作成時にスタイルを定義する、アダプティブフォームのテンプレートの一部として使用されます。

## テーマの削除 {#delete-a-theme}

未使用または不要なテーマを削除するには：

1. オーサーインスタンスにログインします。
1. `http://[Publish Server URL]:[PORT]/crx/de/index.jsp` を開きます。
1. `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]` に移動します。
1. theme フォルダーを削除し、変更を保存します。


## よくある質問 {#faq}

**Q:** テーマフォルダーのカスタマイズをグローバルレベルとコンポーネントレベルの両方で行う場合、どのカスタマイズが優先されますか？

**回答：** テーマレベルとコンポーネントレベルの両方でスタイルを定義すると、コンポーネントレベルで定義されたスタイルが優先されます。

**Q:** カスタムテーマが **[!UICONTROL テーマクライアントライブラリ]**?

**回答：**  カスタムテーマが **[!UICONTROL テーマクライアントライブラリ]** ドロップダウンで、次の手順に従います。

1. カスタムテーマクライアントライブラリを追加した場所に移動します。 推奨パスは次のとおりです。 `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. を開きます。 `.content.xml` ファイルを作成し、次のメタデータを含めます。

   ```
       formstheme:true
       allowproxy:true
   ```

1. ファイルを保存し、テーマを再デプロイします。

## 関連トピック

* [コアコンポーネントベースのアダプティブフォームを作成する](create-an-adaptive-form-core-components.md)
* [ルールエディターを使用して、フォームに動的な動作を追加します](rule-editor.md)
* [コアコンポーネントベースのアダプティブFormsのテーマを作成またはカスタマイズする](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [コアコンポーネントベースのアダプティブFormsのテンプレートを作成する](template-editor.md)
* [アダプティブフォームを作成するか、AEM Sitesページまたはエクスペリエンスフラグメントに追加する](create-or-add-an-adaptive-form-to-aem-sites-page.md)

