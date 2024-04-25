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

AEM 6.1 Communities の場合、サンドボックスをすばやく作成する最も簡単な方法は、コミュニティサイトを作成することです。 参照： [AEM Communitiesの概要](getting-started.md).

開発者向けのもう 1 つの便利なツールは次のとおりです [コミュニティコンポーネントガイド](components-guide.md)を使用すると、Communities のコンポーネントや機能を探索し、迅速にプロトタイプ化することができます。

Web サイトの作成の演習は、Communities の機能を含むAEM web サイトの構造を理解するのに役立つだけでなく、の操作を検討する簡単なページも提供できます [ソーシャルコンポーネントフレームワーク（SCF）](scf.md).

このチュートリアルは、主にAEMを初めて使用し、SCF コンポーネントの使用に関心のある開発者向けです。 SCF サンドボックスサイトの作成については、のチュートリアルに類似した手順を実行します [完全に機能するインターネット Web サイトの作成方法](../../help/sites-developing/website.md) サイト構造（ナビゲーション、ロゴ、検索、ツールバー、子ページのリストなど）に焦点を当てています。

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
>このチュートリアルでは、を使用して作成された機能を持つコミュニティサイトは作成しません [コミュニティサイトコンソール](sites-console.md). 例えば、このチュートリアルでは、ログイン、自己登録、 [ソーシャルログイン](social-login.md)、メッセージング、プロファイルなど。
>
>単純なコミュニティサイトをお勧めする場合は、次の手順に従います [サンプルページの作成](create-sample-page.md) チュートリアル。

## 前提条件 {#prerequisites}

このチュートリアルでは、以下を含む 1 つのAEM オーサーインスタンスと 1 つのAEM パブリッシュインスタンスがインストールされていることを前提としています [最新リリース](deploy-communities.md#latest-releases) （コミュニティ）。

AEM プラットフォームを初めて使用する開発者向けに役立つリンクを以下に示します。

* [はじめに](../../help/sites-deploying/deploy.md#getting-started):AEM インスタンスのデプロイ用。

   * [基本](../../help/sites-developing/the-basics.md):web サイトおよび機能の開発者向け。
   * [作成者がおこなう最初の手順](../../help/sites-authoring/first-steps.md)：ページコンテンツのオーサリング用。

## CRXDE Lite開発環境の使用 {#using-crxde-lite-development-environment}

AEM開発者は、多くの時間を [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) オーサーインスタンス上の開発環境 CRXDE Liteを使用すると、CRX リポジトリへの制限の少ないアクセスが提供されます。 クラシック UI ツールおよびタッチ操作対応 UI コンソールを使用すると、CRX リポジトリの特定の部分への構造化されたアクセスが提供されます。

管理者権限でログインした後、様々な方法でCRXDE Liteにアクセスできます。

1. グローバルナビゲーションから「ナビゲーション」を選択します **[!UICONTROL ツール/CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. から [クラシック UI のようこそページ](http://localhost:4502/welcome.html)を選択し、下にスクロールして **[!UICONTROL CRXDE Lite]** 右側のパネルに表示されます。

   ![クラシック ui-crxde](assets/classic-ui-crxde.png)

3. を直接参照 `CRXDE Lite`: `<server>:<port>/crx/de`

   例えば、ローカルオーサーインスタンスの場合は、次のようになります。 [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Liteを操作するには、開発者または管理者権限でログインする必要があります。 デフォルトの localhost インスタンスの場合は、次を使用してログインできます。

* `username: admin`
* `password: admin`


このログインはタイムアウトし、CRXDE Liteツールバーの右端にあるプルダウンを使用して、定期的に再ログインする必要があります。

ログインしていない場合、JCR リポジトリに移動したり、編集/保存操作を実行したりすることはできません。

***不確かな場合は再ログイン***

![再ログイン](assets/relogin.png)
