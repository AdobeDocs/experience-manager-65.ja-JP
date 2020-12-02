---
title: Web サイト構造のセットアップ
seo-title: Web サイト構造のセットアップ
description: ディレクトリのセットアップ
seo-description: ディレクトリのセットアップ
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 42%

---


# Web サイト構造のセットアップ  {#setup-website-structure}

Web サイトをセットアップするために、後述の手順では、次の場所に作成するフォルダーについて説明します。

* `/apps/an-scf-sandbox`

   ここにカスタムアプリケーションとテンプレートが存在します。

* `/etc/designs/an-scf-sandbox`

   これは、ダウンロード可能なデザイン要素が存在する場所です。

* `/content/an-scf-sandbox`

   ここは、ダウンロード可能なWebページがある場所です。

このチュートリアル内のコードは、アプリケーション、デザインおよびコンテンツについてメインフォルダー名が同じであるという前提に基づきます。Webサイトに別の名前を選択した場合は、`an-scf-sandbox`を必ず選択した名前に置き換えてください。

>[!NOTE]
>
>名前について：
>
>* CRXDEに表示される名前は、アドレス指定可能なコンテンツへのパスを形成するノード名です。
>* ノード名にはスペースを含めることができますが、URIで使用する場合は、スペースを&#39;%20&#39;または&#39;+&#39;としてエンコードする必要があります。
>* ノード名にはハイフンやアンダースコアを含めることができますが、Javaファイル内でパッケージ名として参照する場合はエンコードする必要があります。 ハイフンとアンダースコアは共に、アンダースコアでエスケープされ、その後にUnicode値が続きます。

   >
   >   
   * ハイフンが「_002d」になる
   >   * アンダースコアは「_005f」になります。


## アプリケーションディレクトリ(/apps) {#setup-the-application-directory-apps}の設定

リポジトリの /apps ディレクトリには、/content ディレクトリから提供されるページの動作やレンダリングを実装するコードが格納されます。

/apps ディレクトリは保護され、/content ディレクトリおよび /etc/designs ディレクトリとは異なり、外部からアクセスすることはできません。

1. `/apps/an-scf-sandbox`フォルダーを作成します。

   **[!UICONTROL CRXDE Lite]** を使用して、エクスプローラーペインで次の手順を実行します。

   1. `/apps`フォルダーを選択します。
   1. **[!UICONTROL 「作成]**...」を右クリックするか、**[!UICONTROL 作成…をプルダウンします。]**&#x200B;メニュー。
   1. **[!UICONTROL フォルダの作成を選択…]**.
   1. **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログで、`an-scf-sandbox`と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL components]** サブフォルダーを作成します。

   1. `/apps/an-scf-sandbox`フォルダーを選択します。
   1. **[!UICONTROL 作成/フォルダーを作成]**&#x200B;をクリックします。
   1. **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログで、**[!UICONTROL components]**&#x200B;と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL templates]** サブフォルダーを作成します。

   1. `/apps/an-scf-sandbox`フォルダーを選択します。
   1. **[!UICONTROL 作成/フォルダーを作成]**&#x200B;をクリックします。
   1. **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログで、**[!UICONTROL templates]**&#x200B;と入力します。
   1. 「**[!UICONTROL OK]**」をクリックします。
   1. `/apps/an-scf-sandbox`を選択し直します。
   1. 「**[!UICONTROL すべて保存]**」を選択します。

   他の編集プロセスと同様ですが、保存は頻繁におこなってください。データの入力に問題が発生した場合は、ログインがタイムアウトしたか、以前の編集内容を保存する必要があることが原因である可能性があります。

1. CRXDE Lite のエクスプローラーペインでの構造は、次のようになります。

   ![crxde-template](assets/crxde-template.png)

## デザインディレクトリ(/etc/designs)を設定{#setup-the-design-directory-etc-designs}

/etc/designs ディレクトリには、ページコンテンツと共にダウンロードされる画像、スクリプトおよびスタイルシートが格納されます。

1. クラシックUIのDesignerツールを使用するには、[https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin)を参照します。

   注意：CRXDE Liteを使用して`cq:Page`タイプのノードを作成する場合、アクセス制御とレプリケーションはページのデフォルト設定に設定されません。

1. エクスプローラウィンドウで、**[!UICONTROL Designs]**&#x200B;フォルダーを選択し、**[!UICONTROL 新規]**/**[!UICONTROL 新規ページ]**&#x200B;をクリックします。

   次のように入力します。

   * タイトル：**[!UICONTROL SCF Sandbox]**
   * 名前：**[!UICONTROL an-scf-sandbox]**
   * 「**[!UICONTROL デザインページテンプレート]**」を選択します。

   「**[!UICONTROL 作成]**」をクリックします。

   ![design-template](assets/design-template.png)

1. An SCF Sandbox フォルダーが表示されない場合は、エクスプローラーペインを更新します。

1. CRXDE Lite（http://localhost:4502/crx/de）に戻り、/etc/designs を展開して、「an-scf-sandbox」という名前のノードを表示します。

   CRXDE の右下のペインで、「プロパティ」タブ、「アクセス制御」タブおよび「レプリケーション」タブを表示して、デザインページテンプレートを使用して定義された内容を確認できます。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## コンテンツディレクトリ(/content) {#setup-the-content-directory-content}の設定

リポジトリの /content ディレクトリには、Web サイトコンテンツが格納されます。/contentの下のパスは、ブラウザーリクエストのURLのパスを構成します。

*初期アプリ* の一部として [ページ](initial-app.md#createthepagetemplate) テンプレートを作成した後、テンプレートに基づいて初期ページコンテンツを作成することができる。.  [**>**](initial-app.md)
