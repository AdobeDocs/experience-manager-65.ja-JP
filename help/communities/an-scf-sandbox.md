---
title: SCF サンドボックスの作成
description: このチュートリアルは、主にAEMを初めて使用し、SCF コンポーネントの使用に関心のある開発者向けです。 SCF サンドボックスサイトの作成について順を追って説明します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 3%

---

# SCF サンドボックスの作成  {#create-an-scf-sandbox}

AEM 6.1 Communities の場合、サンドボックスをすばやく作成する最も簡単な方法は、コミュニティサイトを作成することです。 [AEM Communitiesの概要 ](getting-started.md) を参照してください。

開発者にとってもう 1 つの便利なツールは、[ コミュニティコンポーネントガイド ](components-guide.md) です。このガイドを使用すれば、コミュニティのコンポーネントや機能を探索し、迅速にプロトタイプを作成できます。

Web サイトの作成の演習は、Communities の機能を含むAEM web サイトの構造を理解するのに役立ちますが、[ ソーシャルコンポーネントフレームワーク（SCF） ](scf.md) の操作について調べる簡単なページも提供します。

このチュートリアルは、主にAEMを初めて使用し、SCF コンポーネントの使用に関心のある開発者向けです。 ここでは、ナビゲーション、ロゴ、検索、ツールバー、子ページのリスト化など、サイト内の構造に焦点を当てた [ 完全に機能するインターネット web サイトを作成する方法 ](../../help/sites-developing/website.md) のチュートリアルに類似した、SCF サンドボックスサイトの作成について順を追って説明します。

開発はオーサーインスタンスで行われますが、サイトでの実験はパブリッシュインスタンスで行うのが最適です。

このチュートリアルの手順は次のとおりです。

* [Web サイト構造のセットアップ](setup-website.md)
* [初期サンドボックスアプリケーション](initial-app.md)
* [初期サンドボックスコンテンツ](initial-content.md)
* [サンドボックスアプリケーションの開発](develop-app.md)
* [clientlib の追加](add-clientlibs.md)
* [サンドボックスコンテンツの開発](develop-content.md)

>[!CAUTION]
>
>このチュートリアルでは、[Communities サイトコンソール ](sites-console.md) を使用して作成された機能を持つコミュニティサイトは作成しません。 例えば、このチュートリアルでは、ログイン、自己登録、[ ソーシャルログイン ](social-login.md)、メッセージング、プロファイルなどの設定方法については説明しません。
>
>シンプルなコミュニティサイトをお勧めする場合は、[ サンプルページを作成 ](create-sample-page.md) チュートリアルに従ってください。

## 前提条件 {#prerequisites}

このチュートリアルでは、Communities の [ 最新リリース ](deploy-communities.md#latest-releases) を備えた 1 つのAEM オーサーインスタンスと 1 つのAEM パブリッシュインスタンスがインストールされていることを前提としています。

AEM プラットフォームを初めて使用する開発者向けに役立つリンクを以下に示します。

* [ はじめに ](../../help/sites-deploying/deploy.md#getting-started):AEM インスタンスのデプロイ用。

   * [ 基本 ](../../help/sites-developing/the-basics.md):Web サイトや機能の開発者向け。
   * [ 作成者がおこなう最初の手順 ](../../help/sites-authoring/first-steps.md)：ページコンテンツのオーサリング用。

## CRXDE Lite開発環境の使用 {#using-crxde-lite-development-environment}

AEM開発者は、ほとんどの時間をオーサーインスタンスの [&#128279;](../../help/sites-developing/developing-with-crxde-lite.md)0&rbrace;CRXDE Lite&rbrace; 開発環境に費やします。 CRXDE Liteを使用すると、CRX リポジトリへの制限の少ないアクセスが提供されます。 クラシック UI ツールおよびタッチ操作対応 UI コンソールを使用すると、CRX リポジトリの特定の部分への構造化されたアクセスが提供されます。

管理者権限でログインした後、様々な方法でCRXDE Liteにアクセスできます。

1. グローバルナビゲーションから、ナビゲーション **[!UICONTROL ツール/CRXDE Lite]** を選択します。

   ![crxde-lite](assets/tools-crxde.png)

2. [ クラシック UI のようこそページ ](http://localhost:4502/welcome.html) から、下にスクロールして、右側のパネルの **[!UICONTROL CRXDE Lite]** をクリックします。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. `CRXDE Lite`: `<server>:<port>/crx/de` を直接参照します。

   例えば、ローカルオーサーインスタンスの場合：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Liteを操作するには、開発者または管理者権限でログインする必要があります。 デフォルトの localhost インスタンスの場合は、次を使用してログインできます。

* `username: admin`
* `password: admin`


このログインはタイムアウトし、CRXDE Liteツールバーの右端にあるプルダウンを使用して、定期的に再ログインする必要があります。

ログインしていない場合、JCR リポジトリに移動したり、編集/保存操作を実行したりすることはできません。

***不明の場合は、再ログインしてください。***

![ 再ログイン ](assets/relogin.png)
