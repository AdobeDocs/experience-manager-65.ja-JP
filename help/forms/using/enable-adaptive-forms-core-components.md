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
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '968'
ht-degree: 100%

---

# AEM 6.5 Forms でアダプティブフォームコアコンポーネントを有効にする {#enable-adaptive-forms-core-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=ja) |
| AEM 6.5 | この記事 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

アダプティブフォームコアコンポーネントを有効にすると、AEM 6.5 Forms 環境から、[コアコンポーネントベースのアダプティブフォーム](create-an-adaptive-form-core-components.md)および[ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)の作成、公開、配信を開始できます。

AEM 6.5 Forms 環境でアダプティブフォームコアコンポーネントを有効にするには、すべてのオーサーインスタンスとパブリッシュインスタンスで、[AEM アーキタイプ 41 以降](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)をベースにしたプロジェクトを（フォームオプションを有効にして）設定およびデプロイします。

この記事では、AEM 6.5 Forms 環境上で AEM アーキタイプ 41 以降ベースのプロジェクトを設定してデプロイし、アダプティブフォームコアコンポーネントを有効にする詳細な手順を説明します。Forms コアコンポーネントを有効にするための **AEM 6.5** と互換性があるバージョンについては、以下のリストを参照してください。

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
   1. `core.forms.components.version` と `core.forms.components.af.version` のバージョンを [Forms コアコンポーネントの最新](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=ja#aem-as-form-version-history)バージョンに設定します。両者が、表に記載されている **Forms コアコンポーネント**&#x200B;と同じバージョンであることを確認し、[WCM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html?lang=ja)で指定されているように `core.wcm.components.version` のバージョンを設定します。

      >[!WARNING]
      >
      >* バージョン 45 を使用してアーキタイププロジェクトを作成する場合、`[AEM Archetype Project Folder]/pom.xml` では最初、フォームコアコンポーネントのバージョンを 1.1.28 に設定します。アーキタイププロジェクトを作成またはデプロイする前に、フォームコアコンポーネントのバージョンを 1.1.26 に更新します。最新バージョンは、[AEM 6.5 Forms バージョン履歴](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=ja#aem-as-form-version-history)で確認できます。

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
* [コアコンポーネントベースアダプティブフォームのテーマの作成](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [コアコンポーネントベースのアダプティブフォームのテンプレートを作成](template-editor.md)
