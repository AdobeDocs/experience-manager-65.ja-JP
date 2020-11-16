---
title: AEM Brackets Extension
seo-title: AEM Brackets Extension
description: 'null'
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 55%

---


# AEM Brackets Extension{#aem-brackets-extension}

## 概要 {#overview}

AEM Brackets Extension は、AEM コンポーネントとクライアントライブラリを編集するためのスムーズなワークフローを提供し、[Brackets](https://brackets.io/) コードエディターのパワーを活用して、コードエディター内から Photoshop ファイルおよびレイヤーにアクセスできるようにします。この拡張機能によって（Maven や File Vault は不要です）同期が容易になるので、開発者の効率性が向上すると共に、AEM に関する知識が限られているフロントエンド開発者もプロジェクトに参加できます。This extension also provides some support for the [HTML Template Language (HTL)](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html), which takes away the complexity of JSP to make component development easier and more secure.

![chlimage_1-53](assets/chlimage_1-53a.png)

### 特長 {#features}

AEM Brackets Extension の主な機能には次のものがあります。

* 変更されたファイルをAEM開発インスタンスに自動で同期します。
* ファイルとフォルダーの手動の双方向同期。
* プロジェクトの完全なコンテンツパッケージの同期。
* HTL code completion for expressions and `data-sly-*` block statements.

さらに、Brackets には AEM フロントエンド開発者の役に立つ機能が数多く付属しています。

* レイヤー、測定値、色、フォント、テキストなどの情報を PSD ファイルから抽出するための Photoshop ファイルサポート。
* 抽出されたこれらの情報をコード内で再利用しやすくするための PSD からのコードヒント。
* LESSやSCSSなど、CSSプリプロセッサのサポート。
* より具体的なニーズに対応する何百もの追加の拡張。

## インストール {#installation}

### Brackets {#brackets}

AEM Brackets Extension は、Brackets バージョン 1.0 以上をサポートしています。

Download the latest Brackets version from [brackets.io](https://brackets.io/).

### AEM Brackets Extension {#the-extension}

この拡張をインストールするには、次の手順を実行します。

1. Brackets を開きます。**File** メニューで、「**Extension Manager**」を選択します。
1. **検索**&#x200B;バーに「**AEM**」と入力し、AEM Brackets Extension を探します。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 「**インストール**」をクリックします。
1. インストールが完了したら、ダイアログと Extension Manager を閉じます。

## 概要 {#getting-started}

### コンテンツパッケージプロジェクト {#the-content-package-project}

拡張をインストールしたら、Brackets を使用してファイルシステムのコンテンツパッケージフォルダーを開き、AEM コンポーネントの開発を始めることができます。

プロジェクトには、少なくとも次のものが必要です。

1. フォ `jcr_root` ルダー( `myproject/jcr_root`)

1. a `filter.xml` file (e.g. `myproject/META-INF/vault/filter.xml`); for more details about the structure of the `filter.xml` file please see the [Workspace Filter definition](https://jackrabbit.apache.org/filevault/filter.html).

Brackets の **File** メニューで「**Open Folder**」を選択し、`jcr_root` フォルダーまたは親プロジェクトフォルダーを選択します。

>[!NOTE]
>
>If you don&#39;t have of your own a project with a content-package, you can try the [HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). On GitHub, click **Download ZIP**, extract the files locally, and as instructed above, open the `jcr_root` folder in Brackets. Then follow the steps below to setup the **Project Settings**, and finally upload the whole package to your AEM development instance by doing an **Export Content Package** as instructed further down in the Full Content-Package Synchronization section.
>
>After these steps, you should be able to access the `/content/todo.html` URL on your AEM development instance and you can start doing modifications to the code in Brackets and see how, after doing a refresh in the web browser, the changes were immediately synchronized to the AEM server.

### プロジェクト設定 {#project-settings}

コンテンツを AEM 開発インスタンスに、または AEM 開発インスタンスから同期するには、プロジェクト設定を定義する必要があります。This can be done by going to the **AEM** menu and choosing **Project Settings…**

![chlimage_1-55](assets/chlimage_1-55a.png)

プロジェクト設定を使用して、次のものを定義できます。

1. The server URL (e.g. `http://localhost:4502`)
1. 有効なHTTPS証明書を持たないサーバーを許容するかどうか（必要な場合を除き、チェックを外しておく）
1. コンテンツの同期に使用するユーザー名（例：`admin`）
1. The user&#39;s password (e.g. `admin`)

## コンテンツの同期 {#synchronizing-content}

The AEM Brackets Extension provides following types of content synchronization for files and folders that are allowed by the filtering rules defined in `filter.xml`:

### 変更されたファイルの自動同期 {#automated-synchronization-of-changed-files}

これは、変更内容を Brackets から AEM インスタンスへという方向にのみ同期するもので、逆方向には同期しません。

### 手動双方向同期 {#manual-bidirectional-synchronization}

In the Project Explorer, open the contextual menu by right-clicking on any file or folder, and the **Export to Server** or **Import from Server** options can be accessed.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>If the selected entry is outside of the `jcr_root` folder, the **Export to Server** and **Import from Server** contextual menu entries are disabled.

### コンテンツパッケージ全体の同期 {#full-content-package-synchronization}

In the **AEM** menu, the **Export Content Package** or **Import Content Package** options allow to synchronize the whole project with the server.

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同期ステータス {#synchronization-status}

AEM Brackets Extension によって、Brackets ウィンドウの右側のツールバーに、最新の同期ステータスを示す通知アイコンが追加されます。

* 緑 - すべてのファイルが正常に同期されました
* 青 - 同期操作中です
* 黄 - 一部のファイルが同期されませんでした
* 赤 - ファイルがすべて同期されませんでした

通知アイコンをクリックすると、同期された各ファイルのステータスすべてを一覧表示する同期ステータスレポートダイアログが開きます。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>使用する同期方法にかかわらず、`filter.xml` のフィルタリングルールによって「含める」とマークされているコンテンツのみが同期されます。
>
>Additionally, `.vltignore` files are supported for excluding content from synchronizing to and from the repository.

## HTL コードの編集 {#editing-htl-code}

AEM Brackets Extension によって、HTL 属性および式の作成を容易にするオートコンプリートも導入されます。

### 属性のオートコンプリート {#attribute-auto-completion}

1. HTML 属性に「`sly`」と入力します。この属性は、「`data-sly-`」-」にオートコンプリートされます。
1. ドロップダウンリストでこの HTL 属性を選択します。

### 式のオートコンプリート {#expression-auto-completion}

Within an expression `${}`, common variable names are auto-completed.

## 詳細情報 {#more-information}

AEM Brackets Extension はオープンソースのプロジェクトで、Apache License バージョン 2.0 に従って、[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) チームにより GitHub にホストされています。

* コードリポジトリ：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License, version 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

The Brackets code editor is also an open-source project, hosted on GitHub by the [Adobe Systems Incorporated](https://github.com/adobe) organization:

* Code repository: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

ご自由に投稿してください。
