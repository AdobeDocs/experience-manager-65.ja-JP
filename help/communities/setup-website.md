---
title: Web サイト構造のセットアップ
description: 作成するフォルダーを含め、web サイト構造を設定する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# Web サイト構造のセットアップ {#setup-website-structure}

Web サイトを設定するために、以下の手順では、次の場所に作成するフォルダーについて説明します。

* `/apps/an-scf-sandbox`

  ここには、カスタムアプリケーションとテンプレートが存在します。

* `/etc/designs/an-scf-sandbox`

  ダウンロード可能なデザイン要素は、ここに格納されています。

* `/content/an-scf-sandbox`

  ダウンロード可能な web ページは、ここに格納されます。

このチュートリアルのコードは、アプリケーション、デザインおよびコンテンツでメインフォルダー名が同じであることに依存しています。 Web サイトに他の名前を選択した場合は、常に `an-scf-sandbox` を選択した名前に置き換えます。

>[!NOTE]
>
>名前について：
>
>* CRXDE に表示される名前は、アドレス可能なコンテンツへのパスを形成するノード名です。
>* ノード名にはスペースを含めることができますが、URI で使用する場合、スペースは&#39;%20&#39;または&#39;+&#39;としてエンコードする必要があります。
>* ノード名にはハイフンやアンダースコアを含めることができますが、Java™ ファイル内でパッケージ名として参照する場合はエンコードする必要があります。 ハイフンとアンダースコアは、アンダースコアの後に Unicode 値を付けることでエスケープされます。
>
>   * ハイフンは&#39;_002d&#39;になります
>   * アンダースコアは「_005f」になります

## アプリケーションディレクトリ （/apps）を設定 {#setup-the-application-directory-apps}

リポジトリの/apps ディレクトリには、が格納されているコードが含まれています。このコードにより、/content ディレクトリから提供されるページの動作とレンダリングが実装されます。

/apps ディレクトリは保護されており、/content ディレクトリや/etc/designs ディレクトリのように公開アクセスはできません。

1. フォルダー `/apps/an-scf-sandbox` 作成します。

   エクスプローラーウィンドウで **[!UICONTROL CRXDE Lite]** を使用する

   1. `/apps` フォルダーを選択します。
   1. 「**[!UICONTROL 作成]**」を右クリックするか、「**[!UICONTROL 作成]**」メニューをプルダウンします。
   1. 「**[!UICONTROL フォルダーを作成…]**」を選択します。
   1. **[!UICONTROL フォルダーを作成]** ダイアログで、`an-scf-sandbox` と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL components]** サブフォルダーを作成します。

   1. `/apps/an-scf-sandbox` フォルダーを選択します。
   1. **[!UICONTROL 作成/フォルダーを作成]** をクリックします。
   1. **[!UICONTROL フォルダーを作成]** ダイアログで、**[!UICONTROL components]** と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL templates]** サブフォルダーを作成します。

   1. `/apps/an-scf-sandbox` フォルダーを選択します。
   1. **[!UICONTROL 作成/フォルダーを作成]** をクリックします。
   1. **[!UICONTROL フォルダーを作成]** ダイアログで、**[!UICONTROL templates]** と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。
   1. `/apps/an-scf-sandbox` を再選択します。
   1. 「**[!UICONTROL すべて保存]**」を選択します。

   他の編集プロセスと同様に、頻繁に保存する必要があります。 データ入力で問題が発生した場合は、ログインがタイムアウトしたか、以前の編集内容を保存する必要がある可能性があります。

1. CRXDE Liteのエクスプローラーパネルの構造は、次のようになります。

   ![crxde-template](assets/crxde-template.png)

## デザインディレクトリ （/etc/designs）を設定します。 {#setup-the-design-directory-etc-designs}

/etc/designs ディレクトリには、ダウンロードする画像、スクリプト、スタイルシートと、ページコンテンツが含まれています。

1. クラシック UI でDesigner ツールを使用するには、[https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin) を参照します。

   注意：CRXDE Liteを使用して `cq:Page` 型のノードを作成する場合、アクセス制御およびレプリケーションはページのデフォルト設定に設定されません。

1. エクスプローラーウィンドウで、**[!UICONTROL Designs]** フォルダーを選択して **[!UICONTROL 新規]**/**[!UICONTROL 新しいページ]** をクリックします。

   Enter:

   * タイトル：**[!UICONTROL SCF サンドボックス]**
   * 名前：**[!UICONTROL an-scf-sandbox]**
   * **[!UICONTROL デザインページテンプレート]**」を選択します。

   「**[!UICONTROL 作成]**」をクリックします。

   ![design-template](assets/design-template.png)

1. 「SCF サンドボックス」フォルダーが表示されない場合は、エクスプローラーペインを更新します。

1. CRXDE Lite（http:// localhost:4502/crx/de）に戻り、/etc/designs を展開して「an-scf-sandbox」という名前のノードを表示します。

   CRXDE の右下のペインには、「プロパティ」タブ、「アクセス制御」タブ、「レプリケーション」タブが表示され、デザインページテンプレートを使用して定義された内容を確認できます。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## コンテンツディレクトリ （/content）を設定します {#setup-the-content-directory-content}

リポジトリ内の/content ディレクトリは、web サイトコンテンツが存在する場所です。 /content の下のパスは、ブラウザーリクエストの URL のパスで構成されます。

*後* 初期アプリケーションの一部として [&#x200B; ページテンプレート &#x200B;](initial-app.md#createthepagetemplate) を作成した後、テンプレートに基づいて初期ページコンテンツを作成できる… [**⇒**](initial-app.md)
