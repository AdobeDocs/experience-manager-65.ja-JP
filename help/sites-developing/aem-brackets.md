---
title: AEM Brackets 拡張
seo-title: AEM Brackets Extension
description: AEM Brackets 拡張
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 99%

---

# AEM Brackets 拡張{#aem-brackets-extension}

## 概要 {#overview}

AEM Brackets Extension は、AEM コンポーネントとクライアントライブラリを編集するためのスムーズなワークフローを提供し、[Brackets](https://brackets.io/) コードエディターのパワーを活用して、コードエディター内から Photoshop ファイルおよびレイヤーにアクセスできるようにします。この拡張機能によって（Maven や File Vault は不要です）同期が容易になるので、開発者の効率性が向上すると共に、AEM に関する知識が限られているフロントエンド開発者もプロジェクトに参加できます。この拡張機能は、[HTML Template Language（HTL）](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)のサポートも提供しており、複雑な JSP を使用しない、より手軽でセキュアなコンポーネント開発を可能にします。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 機能 {#features}

AEM Brackets Extension の主な機能には次のものがあります。

* 変更されたファイルの AEM 開発インスタンスへの自動同期。
* ファイルおよびフォルダーの手動双方向同期。
* プロジェクトのコンテンツパッケージ全体の同期。
* 式および `data-sly-*` ブロックステートメントの HTL コードコンプリート。

さらに、Brackets には AEM フロントエンド開発者の役に立つ機能が数多く付属しています。

* レイヤー、測定値、色、フォント、テキストなどの情報を PSD ファイルから抽出するための Photoshop ファイルサポート。
* 抽出されたこれらの情報をコード内で再利用しやすくするための PSD からのコードヒント。
* LESS および SCSS などの CSS プリプロセッサーサポート。
* より具体的なニーズに対応する何百もの追加の拡張。

## インストール {#installation}

### Brackets {#brackets}

AEM Brackets Extension は、Brackets バージョン 1.0 以上をサポートしています。

最新バージョンの Brackets を [brackets.io](https://brackets.io/) からダウンロードしてください。

### AEM Brackets Extension {#the-extension}

この拡張をインストールするには、次の手順を実行します。

1. Brackets を開きます。**File** メニューで、「**Extension Manager**」を選択します。
1. **検索**&#x200B;バーに「**AEM**」と入力し、AEM Brackets Extension を探します。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 「**インストール**」をクリックします。
1. インストールが完了したら、ダイアログと Extension Manager を閉じます。

## はじめに {#getting-started}

### コンテンツパッケージプロジェクト {#the-content-package-project}

拡張をインストールしたら、Brackets を使用してファイルシステムのコンテンツパッケージフォルダーを開き、AEM コンポーネントの開発を始めることができます。

プロジェクトには、少なくとも次のものが必要です。

1. `jcr_root` フォルダー（例：`myproject/jcr_root`）

1. `filter.xml` ファイル（例：`myproject/META-INF/vault/filter.xml`）。`filter.xml` ファイルの構造について詳しくは、[ワークスペースフィルターの定義](https://jackrabbit.apache.org/filevault/filter.html)を参照してください。

Brackets の **File** メニューで「**Open Folder**」を選択し、`jcr_root` フォルダーまたは親プロジェクトフォルダーを選択します。

>[!NOTE]
>
>コンテンツパッケージを含むプロジェクトを所有していない場合は、[HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc) を使用できます。GitHub で、「**Download ZIP**」をクリックし、ファイルをローカルに抽出し、上記の説明に従って Brackets で `jcr_root` フォルダーを開きます。次に、以下の手順に従って&#x200B;**プロジェクト設定**&#x200B;を行い、最後に「コンテンツパッケージ全体の同期」セクションの下部の説明に従って「**Export Content Package**」を実行して、パッケージ全体を AEM 開発インスタンスにアップロードします。
>
>これらの手順が完了したら、AEM 開発インスタンス上の URL `/content/todo.html` にアクセスし、Brackets でコード変更を開始できるようになり、web ブラウザーを更新することで変更内容がただちに AEM サーバーに同期されることを確認できます。

### プロジェクト設定 {#project-settings}

コンテンツを AEM 開発インスタンスに、または AEM 開発インスタンスから同期するには、プロジェクト設定を定義する必要があります。プロジェクト設定の定義は、**AEM** メニューに移動し、「**プロジェクト設定**」を選択しておこないます。

![chlimage_1-55](assets/chlimage_1-55a.png)

プロジェクト設定を使用して、次を定義できます。

1. サーバー URL（例：`http://localhost:4502`）
1. 有効な HTTPS 証明書がないサーバーを許容するかどうか（必要ない場合はオフのままにしてください）
1. コンテンツの同期に使用するユーザー名（例：`admin`）
1. ユーザーのパスワード（例：`admin`）

## コンテンツの同期 {#synchronizing-content}

AEM Brackets Extension は、`filter.xml` で定義されているフィルタリングルールによって許可されているファイルおよびフォルダーに対して、次のタイプのコンテンツ同期を提供します。

### 変更されたファイルの自動同期 {#automated-synchronization-of-changed-files}

これは、変更内容を Brackets から AEM インスタンスへという方向にのみ同期するもので、逆方向には同期しません。

### 手動双方向同期 {#manual-bidirectional-synchronization}

Project Explorer で、任意のファイルまたはフォルダーを右クリックしてコンテキストメニューを開き、「**サーバーにエクスポート**」または「**サーバーからインポート**」オプションにアクセスできます。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>選択したエントリが `jcr_root` フォルダー外にある場合、コンテキストメニュー項目「**サーバーにエクスポート**」および「**サーバーからインポート**」は無効になります。

### コンテンツパッケージ全体の同期 {#full-content-package-synchronization}

**AEM** メニューで、「**コンテンツパッケージのエクスポート**」または「**コンテンツパッケージのインポート**」オプションを使用して、プロジェクト全体をサーバーと同期できます。

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
>さらに、リポジトリーへの同期およびリポジトリーからの同期からコンテンツを除外するために、`.vltignore` ファイルがサポートされています。

## HTL コードの編集 {#editing-htl-code}

AEM Brackets Extension によって、HTL 属性および式の作成を容易にするオートコンプリートも導入されます。

### 属性のオートコンプリート {#attribute-auto-completion}

1. HTML 属性に「`sly`」と入力します。この属性は、「`data-sly-`」にオートコンプリートされます。
1. ドロップダウンリストでこの HTL 属性を選択します。

### 式のオートコンプリート {#expression-auto-completion}

式 `${}` 内で、一般的な変数名がオートコンプリートされます。

## 詳細情報 {#more-information}

AEM Brackets Extension はオープンソースのプロジェクトで、Apache License バージョン 2.0 に従って、[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) チームにより GitHub にホストされています。

* コードリポジトリー：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License バージョン 2.0：[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets コードエディターもオープンソースのプロジェクトで、[Adobe Systems Inc](https://github.com/adobe)により GitHub にホストされています。

* コードリポジトリー：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

ご自由に投稿してください。
