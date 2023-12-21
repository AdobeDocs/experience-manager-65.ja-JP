---
title: AEM 6.5 Forms でアダプティブフォームコアコンポーネントを有効にする方法
description: AEM 6.5 Forms 環境でアダプティブフォームコアコンポーネントを有効にする手順ガイドです。
keywords: コアコンポーネントの有効化, コアコンポーネントアダプティブフォーム, コアコンポーネント 6.5, アダプティブフォームコアコンポーネント（AEM 6.5）, AF コアコンポーネント（AEM 6.5）, AEM 6.5 Forms コアコンポーネント
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 84%

---

# AEM 6.5 Forms でアダプティブフォームコアコンポーネントを有効にする {#enable-adaptive-forms-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=ja) |
| AEM 6.5 | この記事 |

**適用先：**✅ アダプティブフォームのコアコンポーネント ❎ アダプティブフォームの基盤コンポーネント

アダプティブフォームコアコンポーネントを有効にすると、AEM 6.5 Forms 環境から、[コアコンポーネントベースのアダプティブフォーム](create-an-adaptive-form-core-components.md)および[ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)の作成、公開、配信を開始できます。

AEM 6.5 Forms環境でアダプティブFormsコアコンポーネントを有効にするには、 [AEM Archetype 41 以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) すべてのオーサーインスタンスとパブリッシュインスタンス上の（フォームオプションが有効な）プロジェクトをベースにする。

この記事では、AEM 6.5 Forms環境上のAEM Archetype 41 以降ベースのプロジェクトを設定してデプロイし、アダプティブFormsコアコンポーネントを有効にする詳細な手順を説明します。 以下のリストを参照して、 **AEM 6.5** Formsコアコンポーネントを有効にする互換性のあるバージョン：

## 前提条件 {#prerequisites}

AEM 6.5 Forms 環境でアダプティブフォームコアコンポーネントを有効にする前に、以下の操作が必要です。

* [AEM 6.5 Forms サービスパック 16（6.5.16.0）以降にアップグレードします](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja)。

* [Apache Maven](https://maven.apache.org/download.cgi) の最新リリースをインストールします。

* プレーンテキストエディターをインストールします。例えば Microsoft Visual Studio Code などです。

## 最新の AEM アーキタイプをベースにしたプロジェクトの作成とデプロイ

AEM アーキタイプ 41 [以降](https://github.com/adobe/aem-project-archetype)をベースにしたプロジェクトを作成し、すべてのオーサーインスタンスとパブリッシュインスタンスにデプロイするには：

1. AEM 6.5 Forms インスタンスをホストして実行しているコンピューターに、管理者としてログインします。
1. コマンドプロンプトまたはターミナルを開き、次のコマンドを実行して AEM アーキタイププロジェクトを作成します（フォームオプションを有効にします）。

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

   * Linux または Apple macOS

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

   * `aemVersion` プロパティの値は、`6.5.15.0` からそれ以外に変更しないでください。

   * `archetypeVersion` プロパティを `41` 以降に設定します。最新バージョンについては、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)ドキュメントの必要システム構成の節を参照してください。

   * `appTitle`、`appId`、`groupId`などの、環境に固有の値を反映するようにコマンドを更新します。また、`includeFormsenrollment` プロパティの値を `y` に設定します。フォームポータルを使用する場合は、`includeExamples=y` オプションを設定して、フォームポータルのコアコンポーネントをプロジェクトに含めます。


1. （アーキタイプバージョン 41 ベースのプロジェクトの場合のみ）AEM アーキタイププロジェクトの作成後に、コアコンポーネントベースのアダプティブフォームのテーマを有効にします。テーマを有効にするには、次の手順を実行します。

   1. [AEM Archetype Project Folder]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html を編集用に開きます。

   1. 21 行目に次のコードを追加します。

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![21 行目に上記のコードを追加したところ](/help/forms/using/assets/code-to-enable-themes.png)

   1. ファイルを保存して閉じます。

1. 最新バージョンの Forms コアコンポーネントを含めるようにプロジェクトを更新します。

   1. [AEM Archetype Project Folder]/pom.xml を編集用に開きます。
   1. のバージョンを設定 `core.forms.components.version` および `core.forms.components.af.version` から [最新のFormsコアコンポーネント](https://github.com/adobe/aem-core-forms-components/tree/release/650#system-requirements) のバージョンと両方がと同じバージョンであることを確認します。 **Forms Core Components** 表に記載されている、およびセットバージョンの `core.wcm.components.version` 以下で指定されたように **WCM コアコンポーネント**.

      >[!WARNING]
      >
      >* でアーキタイププロジェクトを作成する場合 `version 45`、 [AEM Archetype プロジェクトフォルダー]/pom.xmlは最初に、フォームコアコンポーネントのバージョンをに設定します。 `1.1.28`. アーキタイププロジェクトを構築またはデプロイする前に、フォームコアコンポーネントのバージョンをに更新します。 `1.1.26`.


      >[!NOTE]
      >
      >* その他のトポロジをセットアップする場合は、Dispatcher レイヤーの送信、事前入力、およびその他の URL を必ず許可リストに登録してください。

   1. ファイルを保存して閉じます。


1. AEM アーキタイププロジェクトが正常に作成されたら、環境用のデプロイメントパッケージをビルドします。パッケージをビルドするには、以下を実行します。

   1. AEM アーキタイププロジェクトのルートディレクトリに移動します。

   1. 次のコマンドを実行して、環境に対応する AEM アーキタイププロジェクトをビルドします。

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   AEM アーキタイププロジェクトが正常にビルドされると、AEM パッケージが生成されます。パッケージは、[AEM Archetype Project Folder]\all\target\[appid].all-[version].zip になります。

1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を使用して、[AEM Archetype Project Folder]\all\target\[appid].all-[version].zip パッケージをすべてのオーサーインスタンスとパブリッシュインスタンスにデプロイします。

>[!NOTE]
>
>
>
> * パブリッシュインスタンスでログインダイアログにアクセスできない場合に、パッケージマネージャーを使用してパッケージをインストールするには、ログインに URL `http://[Publish Server URL]:[PORT]/system/console` を使用してみてください。これにより、パブリッシュインスタンスのログインページにアクセスして、インストールプロセスを続行できます。
> * 環境にデプロイした後で、アーキタイププロジェクトを削除または破棄しないでください。カスタマイズされた新しいアダプティブフォームコアコンポーネントテーマを環境に追加するには、アーキタイププロジェクトが必要です。

お使いの環境でコアコンポーネントが有効になります。空のコアコンポーネントベースのアダプティブフォームテンプレートと Canvas 3.0 テーマが使用中の環境にデプロイされ、[コアコンポーネントベースのアダプティブフォームを作成](create-an-adaptive-form-core-components.md)できるようになります。

## よくある質問

### コアコンポーネントとは

[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)は、web サイト開発時間の短縮とメンテナンスコストの削減を実現する、AEM の標準化された web コンテンツ管理（WCM）コンポーネントのセットです。

### コアコンポーネントを有効にすると、どのような機能が追加されますか？


使用中の環境でアダプティブフォームのコアコンポーネントを有効にすると、空のコアコンポーネントベースのアダプティブフォームテンプレートと Canvas 3.0 テーマが環境に追加されます。お使いの環境でアダプティブフォームのコアコンポーネントを有効にすると、次の操作を実行できます。

* コアコンポーネントベースのアダプティブフォームの作成。
* コアコンポーネントベースのアダプティブフォームテンプレートの作成。
* コアコンポーネントベースのアダプティブフォームテンプレート用のカスタムテーマの作成。
* コアコンポーネントベースのアダプティブフォームの JSON 表現を、フォームのヘッドレス表現を必要とするモバイル、web、ネイティブアプリ、サービスなどのチャネルに提供。

## 次の手順

* [コアコンポーネントベースのアダプティブフォームを作成](/help/forms/using/create-an-adaptive-form-core-components.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームを作成または追加](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [コアコンポーネントベースのアダプティブフォームのテーマを作成](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [コアコンポーネントベースのアダプティブフォームのテンプレートを作成](template-editor.md)
