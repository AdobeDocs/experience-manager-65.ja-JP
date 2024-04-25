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

このチュートリアルのコードは、アプリケーション、デザインおよびコンテンツでメインフォルダー名が同じであることに依存しています。 Web サイトに他の名前を選択した場合は、常に `an-scf-sandbox` 選択した名前で。

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

1. 作成 `/apps/an-scf-sandbox` フォルダー。

   使用 **[!UICONTROL CRXDE Lite]**&#x200B;エクスプローラーパネル内

   1. 「」を選択します `/apps` フォルダー。
   1. 右クリック **[!UICONTROL 作成]**...または、 **[!UICONTROL 作成…]** メニュー。
   1. を選択 **[!UICONTROL フォルダーの作成…]**.
   1. が含まれる **[!UICONTROL フォルダーを作成]** ダイアログ、を入力 `an-scf-sandbox`.
   1. 「**[!UICONTROL OK]**」をクリックします。

1. 作成 **[!UICONTROL components]** サブフォルダー。

   1. 「」を選択します `/apps/an-scf-sandbox` フォルダー。
   1. クリック **[!UICONTROL 作成/フォルダーを作成]**.
   1. が含まれる **[!UICONTROL フォルダーを作成]** ダイアログ、を入力 **[!UICONTROL components]**.
   1. 「**[!UICONTROL OK]**」をクリックします。

1. 作成 **[!UICONTROL templates]** サブフォルダー。

   1. 「」を選択します `/apps/an-scf-sandbox` フォルダー。
   1. クリック **[!UICONTROL 作成/フォルダーを作成]**.
   1. が含まれる **[!UICONTROL フォルダーを作成]** ダイアログ、を入力 **[!UICONTROL templates]**.
   1. 「**[!UICONTROL OK]**」をクリックします。
   1. 再選択 `/apps/an-scf-sandbox`.
   1. 「**[!UICONTROL すべて保存]**」を選択します。

   他の編集プロセスと同様に、頻繁に保存する必要があります。 データ入力で問題が発生した場合は、ログインがタイムアウトしたか、以前の編集内容を保存する必要がある可能性があります。

1. CRXDE Liteのエクスプローラーパネルの構造は、次のようになります。

   ![crxde-template](assets/crxde-template.png)

## デザインディレクトリ （/etc/designs）を設定します。 {#setup-the-design-directory-etc-designs}

/etc/designs ディレクトリには、ダウンロードする画像、スクリプト、スタイルシートと、ページコンテンツが含まれています。

1. クラシック UI の Designer ツールを使用するには、を参照してください。 [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   注意：タイプのノードを作成するためにCRXDE Liteを使用する場合 `cq:Page`の場合、アクセス制御とレプリケーションはページのデフォルト設定には設定されません。

1. エクスプローラーペインで、 **[!UICONTROL デザイン]** フォルダーを選択し、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**.

   Enter:

   * タイトル： **[!UICONTROL SCF サンドボックス]**
   * 名前： **[!UICONTROL an-scf-sandbox]**
   * を選択 **[!UICONTROL ページテンプレートのデザイン]**

   「**[!UICONTROL 作成]**」をクリックします。

   ![design-template](assets/design-template.png)

1. 「SCF サンドボックス」フォルダーが表示されない場合は、エクスプローラーペインを更新します。

1. CRXDE Lite（http:// localhost:4502/crx/de）に戻り、/etc/designs を展開して「an-scf-sandbox」という名前のノードを表示します。

   CRXDE の右下のペインには、「プロパティ」タブ、「アクセス制御」タブ、「レプリケーション」タブが表示され、デザインページテンプレートを使用して定義された内容を確認できます。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## コンテンツディレクトリ （/content）を設定します {#setup-the-content-directory-content}

リポジトリ内の/content ディレクトリは、web サイトコンテンツが存在する場所です。 /content の下のパスは、ブラウザーリクエストの URL のパスで構成されます。

*後* この [ページテンプレート](initial-app.md#createthepagetemplate) は初期アプリケーションの一部として作成され、初期ページコンテンツはテンプレートに基づいて作成でき…す。 [**⇒**](initial-app.md)
