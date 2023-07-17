---
title: AEM 6.5 FormsでアダプティブFormsコアコンポーネントを有効にするにはどうすればよいですか？
seo-title: How to enable Adaptive Forms Core Components on AEM 6.5 Forms?
description: AEM 6.5 Forms環境でアダプティブFormsコアコンポーネントを有効にする手順ガイドです。
seo-description: Step-by-Step guide to help you enable Adaptive Forms Core Components on an AEM 6.5 Forms environment.
keywords: コアコンポーネント、コアコンポーネントアダプティブForms、コアコンポーネント 6.5、アダプティブFormsコアコンポーネント (AEM 6.5)、AF コアコンポーネント (AEM 6.5、AEM 6.5 Formsコアコンポーネント ) の有効化
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: daf97f3d5c5f3c92ff5caeccff583e54f3f57364
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 6%

---


# AEM 6.5 FormsでのアダプティブFormsコアコンポーネントの有効化 {#enable-adaptive-forms-core-components}

アダプティブFormsコアコンポーネントを有効にすると、作成、公開、配信を開始できます [コアコンポーネントベースのアダプティブForms](create-an-adaptive-form-core-components.md) および [ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp) AEM 6.5 Forms環境から

AEM 6.5 Forms環境で HAdaptive Formsコアコンポーネントを有効にするには、 [AEM Archetype 41 以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) すべてのオーサーインスタンスとパブリッシュインスタンス上の（フォームオプションが有効な）プロジェクトをベースにする。

この記事では、AEM 6.5 Forms環境上のAEM Archetype 41 以降ベースのプロジェクトを設定してデプロイし、アダプティブFormsコアコンポーネントを有効にする詳しい手順を説明します。


## 前提条件 {#prerequisites}

AEM 6.5 Forms環境でアダプティブFormsコアコンポーネントを有効にする前に、次の手順を実行します。

* [AEM 6.5 Forms Service Pack 16(6.5.16.0) 以降にアップグレードします。](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* 最新リリースのをインストールする [Apache Maven](https://maven.apache.org/download.cgi).

* プレーンテキストエディターをインストールします。 例： Microsoft Visual Studio Code。

## 最新のAEMアーキタイプベースのプロジェクトを作成してデプロイする

AEMアーキタイプ 41 を作成するには、以下を実行します。 [後](https://github.com/adobe/aem-project-archetype) ベースのプロジェクトを作成し、すべてのオーサーインスタンスとパブリッシュインスタンスにデプロイします。

1. AEM 6.5 Formsインスタンスをホストし、実行しているコンピューターに、管理者としてログインします。
1. コマンドプロンプトまたはターミナルを開き、次のコマンドを実行してAEM Archetype プロジェクトを作成します（フォームオプションが有効な状態）。

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux またはApple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   上記のコマンドを実行する際は、次の点を考慮してください。

   * この `aemVersion` プロパティ `6.5.15.0` 他の何かに

   * を `archetypeVersion` プロパティを `41` または後で。 最新バージョンについては、 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) ドキュメント。

   * コマンドを更新して、 `appTitle`, `appId`、および `groupId`. また、  `includeFormsenrollment` プロパティを `y`. Forms Portal を使用している場合、 `includeExamples=y` Forms Portal コアコンポーネントをプロジェクトに含めるオプション。


1. （アーキタイプバージョン 41 ベースのプロジェクトのみ）AEMアーキタイププロジェクトを作成したら、コアコンポーネントベースのアダプティブFormsのテーマを有効にします。 テーマを有効にするには：

   1. を開きます。 [AEM Archetype プロジェクトフォルダー]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html編集用：

   1. 21 行目に次のコードを追加します。

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![上記のコードを 21 行目に追加します。](/help/forms/using/assets/code-to-enable-themes.png)

   1. ファイルを保存して閉じます。

1. プロジェクトを更新して、Formsコアコンポーネントの最新バージョンを含めます。

   1. を開きます。 [AEM Archetype プロジェクトフォルダー]/pom.xmlを参照してください。
   1. のバージョンを設定 `core.forms.components.version` および `core.forms.components.af.version` から [最新のFormsコアコンポーネント](https://github.com/adobe/aem-core-forms-components/tree/release/650) バージョン。

   1. ファイルを保存して閉じます。


1. AEMアーキタイププロジェクトが正常に作成されたら、環境用のデプロイメントパッケージを構築します。 パッケージをビルドするには：

   1. AEMアーキタイププロジェクトのルートディレクトリに移動します。

   1. 次のコマンドを実行して、環境用のAEM Archetype プロジェクトを構築します。

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   AEMアーキタイププロジェクトが正常に構築されたら、AEMパッケージが生成されます。 パッケージは、次の場所にあります。 [AEM Archetype プロジェクトフォルダー]\all\target\[appid].all-[version].zip

1. 以下を使用： [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja) をデプロイするには [AEM Archetype プロジェクトフォルダー]\all\target\[appid].all-[version]すべてのオーサーインスタンスとパブリッシュインスタンス上に.zip パッケージを作成します。

>[!NOTE]
>
>
>
> * パブリッシュインスタンスでログインダイアログにアクセスできない場合は、パッケージマネージャーを使用してパッケージをインストールするには、次の URL を使用してみてください。 `http://[Publish Server URL]:[PORT]/system/console` ログインします。 これにより、パブリッシュインスタンスのログインページにアクセスして、インストールプロセスを続行できます。
> * 環境にデプロイした後で、アーキタイププロジェクトを削除または破棄しないでください。 カスタマイズされた新しいアダプティブFormsコアコンポーネントテーマを環境に追加するには、アーキタイププロジェクトが必要です。

コアコンポーネントは、お使いの環境で有効になっています。 空のコアコンポーネントベースのアダプティブフォームテンプレートと Canvas 3.0 テーマが環境にデプロイされ、次の操作が可能になります。 [コアコンポーネントベースのアダプティブFormsの作成](create-an-adaptive-form-core-components.md).

## よくある質問

### コアコンポーネントとは

この [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) は、AEMの開発時間を短縮し、Web サイトのメンテナンスコストを削減するための、標準化された Web コンテンツ管理 (WCM) コンポーネントのセットです。

### コアコンポーネントを有効にすると、どのような機能が追加されるのですか？


お使いの環境でアダプティブFormsコアコンポーネントを有効にすると、空のコアコンポーネントベースのアダプティブフォームテンプレートとキャンバス 3.0 テーマが環境に追加されます。 お使いの環境でアダプティブFormsコアコンポーネントを有効にすると、次の操作を実行できます。

* コアコンポーネントベースのアダプティブFormsを作成します。
* コアコンポーネントベースのアダプティブフォームテンプレートを作成します。
* コアコンポーネントベースのアダプティブフォームテンプレート用にカスタムテーマを作成します。
* コアコンポーネントベースのアダプティブフォームの JSON 表現を、モバイル、Web、ネイティブアプリ、フォームのヘッドレス表現を必要とするサービスなどのチャネルに提供する。

## 次の手順

* [コアコンポーネントベースのアダプティブフォームを作成する](/help/forms/using/create-an-adaptive-form-core-components.md)
* [アダプティブフォームを作成するか、AEM Sitesページまたはエクスペリエンスフラグメントに追加する](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [アダプティブFormsに基づくコアコンポーネントのテーマを作成する](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [コアコンポーネントベースのアダプティブFormsのテンプレートを作成する](template-editor.md)