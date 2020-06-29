---
title: SCF サンドボックスの作成
seo-title: SCF サンドボックスの作成
description: このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます
seo-description: このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 342e148ba183782e4c8b0f08328b9d87685ca08e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 57%

---



# SCF サンドボックスの作成  {#create-an-scf-sandbox}


AEM 6.1 Communities 以降では、サンドボックスをすばやく作成するのに最も簡単な方法は、コミュニティサイトを作成することです。See [Getting Started with AEM Communities](getting-started.md).

Another useful tool for developers is the [Community Components guide](components-guide.md), which allows for exploration and quick prototyping of Communities components and features.

The exercise of creating a website can be useful for understanding the structure of an AEM website which may include Communities features, while also providing simple pages on which to explore working with the [social component framework (SCF)](scf.md).

このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができますは、ナビゲーション、ロゴ、検索、ツールバー、子ページのリスト表示などのサイト構造に重点を置いた、 [全機能を果たしたインターネットWebサイト](../../help/sites-developing/website.md) （英語）のチュートリアルに似ています。

オーサーインスタンスで開発を行い、パブリッシュインスタンスでサイトを試してみるのがベストです。

このチュートリアルは次の手順で構成されています。

* [Web サイト構造のセットアップ](setup-website.md)
* [初期サンドボックスアプリケーション](initial-app.md)
* [初期サンドボックスコンテンツ](initial-content.md)
* [サンドボックスアプリケーションの開発](develop-app.md)
* [clientlib の追加](add-clientlibs.md)
* [サンドボックスコンテンツの開発](develop-content.md)

>[!CAUTION]
>
>このチュートリアルでは、[コミュニティサイトコンソール](sites-console.md)を使用して作成するような機能を持つコミュニティサイトは作成しません。For example, this tutorial does not describe how to setup login, self-registration, [social login](social-login.md), messaging, profiles, and so on.
>
>単純なコミュニティサイトが必要な場合は、[サンプルページの作成](create-sample-page.md)のチュートリアルに従ってください。

## 前提条件 {#prerequisites}

このチュートリアルでは、[最新リリース](deploy-communities.md#latest-releases)の Communities を備えた 1 つの AEM オーサーと 1 つの AEM パブリッシュインスタンスがインストールされていることを前提としています。

次に、AEM プラットフォームを初めて使用する開発者にとって役立つリンクをいくつか紹介します。

* [はじめに](../../help/sites-deploying/deploy.md#getting-started): を参照してください。

   * [基本事項](../../help/sites-developing/the-basics.md): を参照してください。
   * [作成者の最初の手順](../../help/sites-authoring/first-steps.md): 」をクリックします。

## CRXDE Lite 開発環境の使用 {#using-crxde-lite-development-environment}

AEM 開発者は、オーサーインスタンス上の [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 開発環境で多くの時間を費やすことになります。CRXDE Liteは、CRXリポジトリへのアクセスに制限が少ないことを提供します。 従来のUIツールとタッチ対応のUIコンソールは、CRXリポジトリの特定の部分に対して、より構造化されたアクセスを提供します。

管理者権限でサインインした後、さまざまな方法で CRXDE Lite にアクセスできます。

1. From global navigation, select navigation **[!UICONTROL Tools > CRXDE Lite]**.

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. From the [classic UI welcome page](http://localhost:4502/welcome.html), scroll down and click **[!UICONTROL CRXDE Lite]** in the right panel.

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. 直接参照 `CRXDE Lite`: `<server>:<port>/crx/de`

   ローカルのオーサーインスタンス上にある場合の例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Lite を使用するには、開発者または管理者権限でサインインする必要があります。デフォルトのlocalhostインスタンスの場合、

* `username: admin`
* `password: admin`


**このログインはタイムアウトになり** 、CRXDe Liteツールバーの右端にあるプルダウンを使用して定期的に再ログインする必要があります。

ログインしていない状態では、JCR リポジトリをナビゲートしたり、編集／保存操作を実行したりすることはできません。

******&#x200B;疑わしい場合は、ログインし直してください。

![chlimage_1-352](assets/chlimage_1-352.png)
