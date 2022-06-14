---
title: SCF サンドボックスの作成
seo-title: Create An SCF Sandbox
description: このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます
seo-description: This tutorial is primarily for developers, new to AEM, who are interested in using SCF components.  It walks through the creation of An SCF Sandbox site
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 54%

---

# SCF サンドボックスの作成  {#create-an-scf-sandbox}


AEM 6.1 Communities 以降では、サンドボックスをすばやく作成するのに最も簡単な方法は、コミュニティサイトを作成することです。詳しくは、 [AEM Communitiesの概要](getting-started.md).

開発者にとっても便利なツールは、 [コミュニティコンポーネントガイド](components-guide.md)：コミュニティのコンポーネントと機能の調査と迅速なプロトタイピングを可能にします。

Web サイトを作成する練習は、コミュニティ機能を含むAEM Web サイトの構造を理解するのに役立ちます。また、を使用して作業を検討するための簡単なページも提供します。 [ソーシャルコンポーネントフレームワーク (SCF)](scf.md).

このチュートリアルは、AEM の知識がなく、SCF コンポーネントの使用に興味を持っている開発者を主な対象としています。手順に従いながら SCF サンドボックスサイトの作成を進めることができます( [完全に機能するインターネット Web サイトを作成する方法](../../help/sites-developing/website.md) これは、ナビゲーション、ロゴ、検索、ツールバー、子ページのリスト表示など、サイト構造に重点を置いたものです。

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
>このチュートリアルでは、[コミュニティサイトコンソール](sites-console.md)を使用して作成するような機能を持つコミュニティサイトは作成しません。例えば、このチュートリアルでは、ログイン、自己登録、 [ソーシャルログイン](social-login.md)、メッセージング、プロファイルなど。
>
>単純なコミュニティサイトが必要な場合は、[サンプルページの作成](create-sample-page.md)のチュートリアルに従ってください。

## 前提条件 {#prerequisites}

このチュートリアルでは、[最新リリース](deploy-communities.md#latest-releases)の Communities を備えた 1 つの AEM オーサーと 1 つの AEM パブリッシュインスタンスがインストールされていることを前提としています。

次に、AEM プラットフォームを初めて使用する開発者にとって役立つリンクをいくつか紹介します。

* [はじめに](../../help/sites-deploying/deploy.md#getting-started):AEMインスタンスをデプロイする場合。

   * [基本](../../help/sites-developing/the-basics.md):web サイトおよび機能の開発者向け
   * [作成者向けの最初の手順](../../help/sites-authoring/first-steps.md):（ページコンテンツをオーサリングするため）

## CRXDE Lite 開発環境の使用 {#using-crxde-lite-development-environment}

AEM 開発者は、オーサーインスタンス上の [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 開発環境で多くの時間を費やすことになります。CRXDE Liteは、CRX リポジトリへのアクセスを制限されていません。 クラシック UI ツールとタッチ操作対応 UI コンソールを使用すると、CRX リポジトリの特定の部分に対して、より構造化されたアクセスを提供できます。

管理者権限でサインインした後、さまざまな方法で CRXDE Lite にアクセスできます。

1. グローバルナビゲーションから、「ナビゲーション」を選択します。 **[!UICONTROL ツール/CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. 次の [クラシック UI のようこそページ](http://localhost:4502/welcome.html)をクリックし、下にスクロールして **[!UICONTROL CRXDE Lite]** をクリックします。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接参照先 `CRXDE Lite`: `<server>:<port>/crx/de`

   ローカルのオーサーインスタンス上にある場合の例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Lite を使用するには、開発者または管理者権限でサインインする必要があります。デフォルトの localhost インスタンスの場合は、を使用してログインできます。

* `username: admin`
* `password: admin`


**注意** このログインがタイムアウトすると、CRXDe Lite ツールバーの右側にあるプルダウンを使用して、定期的に再ログインする必要があります。

ログインしていない状態では、JCR リポジトリをナビゲートしたり、編集／保存操作を実行したりすることはできません。

******&#x200B;疑わしい場合は、ログインし直してください。

![再ログイン](assets/relogin.png)
