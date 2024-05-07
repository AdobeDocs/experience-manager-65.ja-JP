---
title: カスタムアダプティブフォームテーマの作成方法
description: BEM 仕様を使用してアダプティブフォームコアコンポーネントのテーマを作成またはカスタマイズする方法を説明します。
keywords: アダプティブフォームコアコンポーネントのテーマの作成、新しいテーマの作成、テーマのカスタマイズ、新しいテーマのアップロード、Forms でのテーマの使用、テーマの削除、AEM 6.5 Forms でのテーマの作成
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1921'
ht-degree: 100%

---

# アダプティブフォームテーマを作成またはカスタマイズ {#introduction-to-theme}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=ja) |
| AEM 6.5 | この記事 |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

AEM Forms 6.5 では、テーマは、アダプティブフォームのスタイル（ルック＆フィール）を定義するために使用する AEM クライアントライブラリのことです。テーマには、コンポーネントとパネルのスタイルを設定するための詳細情報が含まれています。スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。テーマはアダプティブフォームを参照せずに独立して管理され、複数のアダプティブフォーム間で再利用できます。

## 使用可能なテーマ {#available-theme}

AEM 6.5 環境は、コアコンポーネントベースのアダプティブフォーム向けに、以下のテーマを備えています。

* [カンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

## テーマの構造について {#understanding-structure-of-theme}

テーマは、CSS ファイル、JavaScript ファイル、およびアダプティブフォームのスタイルを定義するリソース（アイコンなど）を網羅するパッケージです。アダプティブフォームのテーマは、次のコンポーネントで構成される特定の組織に従います。

* `src/theme.scss`：このフォルダーには、テーマ全体に大きな影響を与える CSS ファイルが含まれます。テーマのスタイル設定と動作を一元的に定義および管理できます。このファイルを編集するとテーマ全体で共通して適用され、アダプティブフォームと AEM Sites の両方のページの外観と機能を変更することができます。

* `src/site`：このフォルダーには、AEM Sites のページ全体に適用される CSS ファイルが含まれます。これらのファイルは、AEM Sites ページの全体的な機能やレイアウトに影響を与えるコードとスタイルで構成されています。ここで行った変更は、サイトのすべてのページに反映されます。

* `src/components`：このフォルダーの CSS ファイルは、AEMの個々のコアコンポーネント用に設計されています。コンポーネントの各専用フォルダーには、アダプティブフォーム内の特定のコンポーネントのスタイルを設定する `.scss` ファイルが含まれています。例えば、`/src/components/button/_button.scss` ファイルには、アダプティブフォームのボタンコンポーネントのスタイル情報が含まれています。

  ![カンバステーマの構造](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`：このフォルダーには、アイコン、ロゴ、フォントなどの静的ファイルが含まれています。これらのリソースは、テーマの視覚的要素と全体的なデザインを強化するために使用されます。

## テーマを作成

AEM Forms 6.5 は、コアコンポーネントベースのアダプティブフォーム向けに、以下のテーマを備えています。

* [カンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

[これらのテーマをカスタマイズしてテーマを作成](#customize-a-theme-core-components)することができます。

## テーマをカスタマイズ {#customize-a-theme-core-components-based-adaptive-forms}

テーマのカスタマイズとは、テーマのアピアランスを変更し、パーソナライズするプロセスを指します。テーマをカスタマイズすると、デザイン要素、レイアウト、色、テキスト編集、基になるコードに変更を加えることができます。これにより、テーマで提供される基本的な構造と機能を維持しながら、web サイトやアプリケーションに独自のカスタマイズされたアピアランスを作成できます。

>[!NOTE]
>
> * パッケージマネージャーを使用して、すべてのオーサーインスタンスとパブリッシュインスタンスにテーマをデプロイします。
> * テーマのクライアントライブラリの読み込みおよび書き込みは、他のパッケージと同様に、パッケージマネージャーを使用して行われます。

### テーマをカスタマイズするための前提条件 {#prerequisites}

* [環境でのアダプティブフォームコアコンポーネントの有効化](/help/forms/using/enable-adaptive-forms-core-components.md)

* [Apache Maven の最新リリースをインストールします。](https://maven.apache.org/download.cgi) Apache Maven は、主に Java™ プロジェクトで使用されるビルド自動処理ツールです。最新のリリースをインストールすると、テーマのカスタマイズに必要な依存関係が確保されます。

* [Adobe Experience Manager のクライアントライブラリ](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=ja)の作成方法を学ぶAEM は、クライアントライブラリを提供しています。これにより、クライアントサイドコードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義できます。

* プレーンテキストエディターをインストールします。例えば Microsoft® Visual Studio Code などです。Microsoft® Visual Studio Code などのプレーンテキストエディターを使用すると、テーマファイルの編集と変更を行う際に使いやすい環境を利用できます。

* AEM Forms 環境が起動および実行されていることを確認してください。

### テーマのカスタマイズに関する考慮事項 {#consideration}

* テーマをカスタマイズする場合は、お使いの環境で[アダプティブフォームコアコンポーネントの有効化に使用するアーキタイププロジェクト](/help/forms/using/enable-adaptive-forms-core-components.md)を使用していることを確認します。

* アダプティブフォームを公開する際、クライアントライブラリはパブリッシュインスタンスでは自動的に公開されません。アダプティブフォーム内で参照されているクライアントライブラリは、パブリッシュ環境に手動で公開してください。

* アドビでは、クライアントライブラリのクラス名を変更しないことをお勧めします。

### テーマをカスタマイズ {#customize-a-theme-core-components}

テーマの作成またはカスタマイズは、複数の手順で行います。テーマを作成またはカスタマイズするには、次の手順をリスト順に実行します。

1. [テーマを複製](#clone-git-repo-of-theme)
1. [テーマの外観をカスタマイズ](#customize-the-theme)
1. [ローカルデプロイメント用にテーマを準備](#generate-the-clientlib)
1. [テーマをローカル環境にデプロイ](#deploy-the-theme-on-a-local-environment)
1. [テーマを実稼動環境にデプロイ](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

このドキュメントで示す例は、**カンバス**&#x200B;テーマに基づいていますが、任意のテーマを複製し、同じ手順を使用してカスタマイズできます。これらの手順はどのテーマにも適用でき、特定のニーズに応じてテーマを変更できます。

#### 1. テーマの Git リポジトリを複製する {#clone-git-repo-of-theme}

コアコンポーネントベースのアダプティブフォームのテーマを複製するには、次のいずれかのテーマを選択します。

* [キャンバステーマ](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND テーマ](https://github.com/adobe/aem-forms-theme-wknd)
* [イーゼルテーマ](https://github.com/adobe/aem-forms-theme-easel)

次の手順を実行して、テーマを複製します。

1. コマンドプロンプトまたはターミナルウィンドウをローカル開発環境で開きます。

1. `git clone` コマンドを実行して、テーマを複製します。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   [テーマの Git リポジトリのパス]を、テーマの対応する Git リポジトリの実際の URL に置き換えます。

   例えば、カンバステーマを複製するには、次のコマンドを実行します。

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. 「**親フォルダー内のすべてのファイルの作成者を信頼する**」を選択し、「**はい、私は作成者を信頼します**」をクリックします。

コマンドを正常に実行すると、そのテーマのローカルコピーがお使いのコンピューターの `aem-forms-theme-canvas` フォルダーで使用可能になります。

#### 2. テーマをカスタマイズ {#customize-the-theme}

個々のコンポーネントをカスタマイズしたり、テーマのグローバル変数を使用してテーマレベルを変更したりできる柔軟性があります。グローバル変数を変更すると、個々のコンポーネントすべてにカスケードエフェクトが適用されます。例えば、グローバル変数を利用して、アダプティブフォーム内のすべてのコンポーネントの境界線の色を変更したり、鮮やかな塗りつぶし色をコールトゥアクション (CTA) ボタンに適用したりできます。以下の操作を実行できます。

* [テーマレベルのスタイルを設定する](#theme-customization-global-level)

* [コンポーネントレベルのスタイルの設定](#component-based-customization)

##### テーマレベルのスタイルを設定する {#theme-customization-global-level}

`variable.scss` ファイルは、テーマのグローバル変数を含んでいます。これらの変数を更新すると、テーマレベルでスタイル関連の変更ができます。テーマレベルのスタイルを適用するには、次の手順を実行します。

1. `<your-theme-sources>/src/site/_variables.scss` ファイルを編集用に開きます。
1. 任意のプロパティの値を変更します。例えば、デフォルトのエラーの色は赤です。エラーの色を赤から青に変更するには、`$error` 変数の 16 進数カラーコードを変更します。例えば、`$error: #196ee5` のように指定します。

   ![例：エラーの色を青に設定](/help/forms/using/assets/theme-level-changes.png)

1. ファイルを保存して閉じます。


同様に、`variable.scss` ファイルを使って、フォントファミリーとタイプ、テーマおよびフォントカラー、フォントサイズ、テーマ間隔、エラーアイコン、テーマの境界線のスタイルなど、複数のアダプティブフォームコンポーネントに影響を与える変数を設定できます。

##### コンポーネントレベルのスタイルを設定する {#component-based-customization}

また、特定のアダプティブフォームコアコンポーネント（ボタン、チェックボックス、コンテナ、フッターなど）のフォント、カラー、サイズ、その他の CSS プロパティをカスタマイズすることもできます。特定のコンポーネントに関連付けられた CSS ファイルを編集することで、そのスタイルを組織のブランディングに合わせることができます。コンポーネントのスタイルをカスタマイズするには、次の手順を実行します。

1. `<your-theme-sources>/src/components/<component>/<component.scss>` ファイルを編集用に開きます。例えば、ボタンコンポーネントのフォントの色を変更するには、`<your-theme-sources>/src/components/button/button.scss` ファイルを開きます。
1. 必要に応じて値を変更します。例えば、ポインタを合わせたときのボタンコンポーネントの色を緑に変更するには、`cmp-adaptiveform-button__widget:hover` クラスで `color: $white` プロパティの値を 16 進数コード #12b453 またはその他の緑の色合いに変更します。最終的なコードは次のようになります。

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

>[!NOTE]
>
> テーマレベルとコンポーネントレベルの両方でスタイルを定義する場合、コンポーネントレベルで定義されたスタイルが優先されます。

#### 3. デプロイメント用にテーマを準備 {#generate-the-clientlib}

AEM インスタンスにテーマをデプロイするには、テーマをクライアントライブラリに変換する必要があります。テーマをクライアントライブラリに変換するには、次の手順に従います。

1. コマンドプロンプトまたはターミナルウィンドウを開きます。
1. `<your-theme-sources>` フォルダーに移動します。例えば、`C:\aem-forms-theme-canvas` のように指定します。
1. 次のコマンドを実行します。

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   `[yourtheme]` をカスタムテーマの名前に置き換えます。例えば、カスタムテーマの名前が `customcanvastheme` の場合、次のコマンドを実行します。

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   コマンドが正常に実行されると、`themerepo\theme-clientlibs\[yourtheme]` にクライアントライブラリフォルダーが作成されます。

   ![クライアントライブラリの生成](/help/forms/using/assets/clientlib_created.png)


   ![クライアントライブラリの場所](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. ローカル環境にテーマをデプロイ {#deploy-the-theme-on-a-local-environment}

ローカル開発またはテスト環境にテーマをデプロイするには、次の手順に従います。

1. アーキタイププロジェクトの次のパスに、前の節で作成したクライアントライブラリをコピーします。

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. コマンドプロンプトまたはターミナルを開きます。
1. アダプティブフォームのコアコンポーネントを有効にするために使用する AEM アーキタイププロジェクトのルートディレクトリに移動します。
1. 次のコマンドを実行して、環境にカスタムテーマをデプロイします。

   `mvn clean install`

   ![クライアントライブラリのビルド](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. 実稼動環境にテーマをデプロイ {#deploy-theme}

ローカル開発環境でテーマのテストを正常に行うことができたら、オーサーインスタンスとパブリッシュインスタンスの両方を含む実稼動環境にテーマをデプロイする手順を実行できます。実稼動環境にテーマをデプロイするには、次の手順に従います。

1. AEM 環境にログインします。
1. パッケージマネージャーを開きます。デフォルトの URL は `https://localhost:4502/crx/packmgr/index.jsp` です。
1. 「**パッケージをアップロード**」、「**参照**」の順にクリックします。
1. `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip` に移動して選択します。「**開く**」をクリックします。
1. 「インストール」をクリックします。すべての実稼動環境でこの手順を繰り返します。


パッケージがインストールされると、テーマを選択できるようになります。

![テーマクライアントライブラリ](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> パブリッシュインスタンスのログインダイアログにアクセスして、パッケージマネージャーでパッケージをインストールできない場合は、次の URL を使用してログインしてみてください：`http://[Publish Server URL]:[PORT]/system/console`これにより、パブリッシュインスタンスにログインして、インストールプロセスを続行できます。

## アダプティブフォームにテーマを適用 {#using-theme-in-adaptive-form}

アダプティブフォームにテーマを適用するには、次の手順を実行します。

1. AEM オーサーインスタンスにログインします。
1. Experience Manager のログインページに資格情報を入力します。**Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;を選択します。
1. **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。
1. アダプティブフォームコアコンポーネントテンプレートを選択し、「**次へ**」をクリックします。**プロパティを追加**&#x200B;が表示されます。
1. アダプティブフォームの&#x200B;**名前**&#x200B;を指定します。


   >[!NOTE]
   >
   > * デフォルトでは、`adaptiveform.theme.canvas3` のテーマが選択されています。
   > * 別のテーマは&#x200B;**テーマクライアントライブラリ**&#x200B;ドロップダウンメニューから選択できます。

1. 「**作成**」をクリックします。

アダプティブフォームのテーマは、アダプティブフォームの作成時にスタイルを定義する、アダプティブフォームのテンプレートの一部として使用されます。

## テーマを削除 {#delete-a-theme}

未使用または不要なテーマを削除するには：

1. オーサーインスタンスにログインします。
1. `http://[Publish Server URL]:[PORT]/crx/de/index.jsp` を開きます。
1. `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]` に移動します。
1. テーマフォルダーを削除し、変更を保存します。


## よくある質問 {#faq}

**Q**：テーマフォルダーのカスタマイズをグローバルレベルとコンポーネントレベルの両方で行う場合、どちらのカスタマイズが優先されますか？

**A**：テーマレベルとコンポーネントレベルの両方でスタイルを定義すると、コンポーネントレベルで定義されたスタイルが優先されます。

**Q**：カスタムテーマが&#x200B;**[!UICONTROL テーマクライアントライブラリ]**&#x200B;に表示されていない場合、どうすればよいですか？

**A**：カスタムテーマが&#x200B;**[!UICONTROL テーマクライアントライブラリ]**&#x200B;ドロップダウンに表示されない場合は、次の手順に従ってください。

1. カスタムテーマのクライアントライブラリを追加した場所に移動します。推奨パスは `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>` です。

1. `.content.xml` ファイルを開き、次のメタデータを含めます。

   ```
       formstheme:true
       allowproxy:true
   ```

1. ファイルを保存し、テーマを再デプロイします。

## 関連トピック

* [コアコンポーネントベースのアダプティブフォームを作成](create-an-adaptive-form-core-components.md)
* [ルールエディターを使用してフォームに動的な動作を追加](rule-editor.md)
* [コアコンポーネントベースのアダプティブフォームのテーマを作成またはカスタマイズ](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [コアコンポーネントベースのアダプティブフォームのテンプレートを作成](template-editor.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームを作成または追加](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [サンプルのテーマテンプレートおよびフォームデータモデル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)
