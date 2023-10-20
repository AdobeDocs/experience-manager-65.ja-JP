---
title: Web サイト構造のセットアップ
description: 作成するフォルダーを含む Web サイト構造を設定する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# Web サイト構造のセットアップ {#setup-website-structure}

Web サイトを設定するために、以下の手順で、次の場所に作成するフォルダーについて説明します。

* `/apps/an-scf-sandbox`

  カスタムアプリケーションとテンプレートが存在する場所です。

* `/etc/designs/an-scf-sandbox`

  ここに、ダウンロード可能なデザイン要素が配置されます。

* `/content/an-scf-sandbox`

  ダウンロード可能な Web ページが配置される場所です。

このチュートリアルのコードは、アプリケーション、デザイン、コンテンツでメインフォルダー名が同じであることに依存します。 Web サイトに別の名前を選択する場合は、 `an-scf-sandbox` 選択した名前で置き換えます。

>[!NOTE]
>
>名前について：
>
>* CRXDE に表示される名前は、アドレス可能なコンテンツへのパスを形成するノード名です。
>* ノード名にはスペースを含めることができますが、URI で使用する場合は、スペースを「%20」または「+」としてエンコードする必要があります。
>* ノード名にハイフンとアンダースコアを含めることができますが、Java™ファイル内でパッケージ名として参照する場合はエンコードする必要があります。 ハイフンとアンダースコアの両方は、アンダースコアに続いて Unicode 値を付けてエスケープされます。
>
* ハイフンが「_002d」になる
* アンダースコアが「_005f」になる

## アプリケーションディレクトリ (/apps) を設定します {#setup-the-application-directory-apps}

リポジトリの/apps ディレクトリには、 /content ディレクトリから提供されるページの動作とレンダリングを実装するコードが含まれています。

/apps ディレクトリは保護され、/content ディレクトリや/etc/designs ディレクトリと同様に、公開されてアクセスできません。

1. 作成 `/apps/an-scf-sandbox` フォルダー。

   使用 **[!UICONTROL CRXDE Lite]**&#x200B;エクスプローラーペインで、

   1. を選択します。 `/apps` フォルダー。
   1. 右クリック **[!UICONTROL 作成]**...またはプルダウン **[!UICONTROL 作成…]** メニュー。
   1. 選択 **[!UICONTROL フォルダーを作成…]**.
   1. Adobe Analytics の **[!UICONTROL フォルダーを作成]** ダイアログ、入力 `an-scf-sandbox`.
   1. 「**[!UICONTROL OK]**」をクリックします。

1. 作成 **[!UICONTROL コンポーネント]** サブフォルダー。

   1. を選択します。 `/apps/an-scf-sandbox` フォルダー。
   1. クリック **[!UICONTROL 作成/フォルダーを作成]**.
   1. Adobe Analytics の **[!UICONTROL フォルダーを作成]** ダイアログ、入力 **[!UICONTROL コンポーネント]**.
   1. 「**[!UICONTROL OK]**」をクリックします。

1. 作成 **[!UICONTROL テンプレート]** サブフォルダー。

   1. を選択します。 `/apps/an-scf-sandbox` フォルダー。
   1. クリック **[!UICONTROL 作成/フォルダーを作成]**.
   1. Adobe Analytics の **[!UICONTROL フォルダーを作成]** ダイアログ、入力 **[!UICONTROL テンプレート]**.
   1. 「**[!UICONTROL OK]**」をクリックします。
   1. 再選択 `/apps/an-scf-sandbox`.
   1. **[!UICONTROL すべて保存]** を選択します。

   編集プロセスと同様に、頻繁に保存する必要があります。 データの入力に問題が発生した場合は、ログインがタイムアウトしたか、以前の編集内容を保存する必要がある可能性があります。

1. CRXDE Liteのエクスプローラーペインの構造は、次のようになります。

   ![crxde-template](assets/crxde-template.png)

## デザインディレクトリ (/etc/designs) を設定します。 {#setup-the-design-directory-etc-designs}

/etc/designs ディレクトリには、ページコンテンツと共にダウンロードされる画像、スクリプト、スタイルシートが含まれます。

1. クラシック UI で Designer ツールを使用するには、以下を参照します。 [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   注意：ノードを使用してCRXDE Liteタイプのノードを作成する場合 `cq:Page`に値を指定しない場合、「アクセス制御」と「レプリケーション」はページのデフォルト設定に設定されませんでした。

1. エクスプローラウィンドウで、 **[!UICONTROL デザイン]** フォルダーに移動し、次に **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**.

   Enter:

   * タイトル： **[!UICONTROL SCF サンドボックス]**
   * 名前： **[!UICONTROL an-scf-sandbox]**
   * 選択 **[!UICONTROL デザインページテンプレート]**

   「**[!UICONTROL 作成]**」をクリックします。

   ![design-template](assets/design-template.png)

1. 「An SCF Sandbox」フォルダが表示されない場合は、エクスプローラペインを更新します。

1. CRXDE Lite(http:// localhost:4502/crx/de) に戻り、/etc/designs を展開して、「an-scf-sandbox」という名前のノードを表示します。

   CRXDE の右下のウィンドウで、「プロパティ」タブ、「アクセス制御」タブ、「レプリケーション」タブを表示して、デザインページテンプレートを使用して定義された内容を確認できます。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## コンテンツディレクトリ (/content) の設定 {#setup-the-content-directory-content}

リポジトリ内の/content ディレクトリは、Web サイトコンテンツが存在する場所です。 /content の下のパスは、ブラウザーリクエストの URL のパスを構成します。

*後* の [ページテンプレート](initial-app.md#createthepagetemplate) は、初期アプリケーションの一部として作成され、初期ページコンテンツは、テンプレートに基づいて作成できます.... [**⇒**](initial-app.md)
