---
title: clientlib の追加
seo-title: clientlib の追加
description: ClientLibraryFolder の追加
seo-description: ClientLibraryFolder の追加
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# clientlib の追加{#add-clientlibs}

## Add a ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. using **CRXDE Lite**, expand `/etc/designs`

1. 右クリック `an-scf-sandbox` して選択 `Create Node`

   * 名前 : `clientlibs`
   * タイプ : `cq:ClientLibraryFolder`

1. 「**OK**」をクリックします。

![chlimage_1-47](assets/chlimage_1-47.png)

In the **Properties** tab for the new `clientlibs` node, enter the **`categories`**property:

* 名前：**categories**
* タイプ：**String**
* 値：**apps.an-scf-sandbox**
* 「**追加**」をクリックします。
* 「**すべて保存**」をクリックします。

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。IMPORTANT : Add placeholder `js.tx`t and**`css.tx`**t files. （正式にはcq:ClientLibraryFolderが存在しない場合は除きます）。

1. 右クリック **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 「**ファイルを作成...**」を選択します。
1. **名前**&#x200B;を入力： `css.txt`
1. 「**ファイルを作成...**」を選択します。
1. **名前**&#x200B;を入力： `js.txt`
1. 「**すべて保存**」をクリックします。

![chlimage_1-48](assets/chlimage_1-48.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。

```
#base=.
 style.css
```

次に、clientlibsの下にstyle.cssという名前のファイルを作成し、コンテンツを

`body {`

`background-color: #b0c4de;`

`}`

### SCF clientlib の埋め込み {#embed-scf-clientlibs}

**ノードの「**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **embed** を入力します。This embeds the necessary [client-side libraries (clientlibs) for SCF components](/help/communities/client-customize.md#clientlibs-for-scf). このチュートリアルでは、Communitiesコンポーネントに必要なclientlibの多くが追加されます。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1 つのページで 1 つの機能のみを使用する場合は、&lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %> など、その機能の完全な clientlib をページに直接含めることができます。

この場合は、すべてを含め、より基本的なSCFクライアントライブラリを作成者のclientlibとして扱うことをお勧めします。

* 名前 : **`embed`**
* タイプ : **`String`**
* click **`Multi`**
* Value: **`cq.social.scf`**
*&lt;enter> will pop up a dialog
click **[+] **after each entry to add the following clientlib categories:*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * 「**OK**」をクリックします。

* 「**すべて保存**」をクリックします。

![chlimage_1-49](assets/chlimage_1-49.png)

This is how `/etc/designs/an-scf-sandbox/clientlibs` should now appear in the repository :

![chlimage_1-50](assets/chlimage_1-50.png)

### playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

Without including the `apps.an-scf-sandbox` ClientLibraryFolder category on the page, the SCF components will not be functional nor styled as the necessary Javascript(s) and style(s) will not be available.

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![chlimage_1-51](assets/chlimage_1-51.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![chlimage_1-52](assets/chlimage_1-52.png)

インクルードステートメントは、 <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 」セクション <html> script. The default **`foundation head.jsp`** includes a script that can be overlaid : **`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. using **CRXDE Lite**, select **`/libs/foundation/components/page/headlibs.jsp`**

1. 右クリックして「**コピー**」を選択します（または、ツールバーから「コピー」を選択します）。
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. 右クリックして「**貼り付け**」を選択します（または、ツールバーから「貼り付け」を選択します）。
1. double click **`headlibs.jsp`** to open it
1. ファイルの末尾に次の行を追加します。
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 「**すべて保存**」をクリックします。

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Web サイトをブラウザーに読み込み、背景が青の網掛けでないかどうかを確認します。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![chlimage_1-53](assets/chlimage_1-53.png)

### これまでの作業内容の保存 {#saving-your-work-so-far}

この時点では最小限のサンドボックスが存在し、再生中にリポジトリが破損し、再生をやり直す必要が生じた場合に、サーバーのオフ、crx-quickstart/フォルダーの名前の変更や削除、サーバーのオン、アップロード、インストールを行うのに役立ちます。

すぐに操作してみたい場合は、[サンプルページの作成](/help/communities/create-sample-page.md)チュートリアルにこのパッケージがあります。

パッケージを作成するには：

* from CRXDE Lite click the [Package icon](https://localhost:4502/crx/packmgr/)
* 「**パッケージを作成**」をクリックします。

   * パッケージ名：an-scf-sandbox-minimal-pkg
   * バージョン：0.1
   * グループ：&lt;デフォルトのまま>
   * 「**OK**」をクリックします。

* 「**編集**」をクリックします。

   * **フィルタ**タブを選択

      * 「**フィルターを追加**」をクリックします。
      * ルートパス：&lt;参照先** /apps/an-scf-sandbox**>
      * 「**完了**」をクリックします。
      * 「**フィルターを追加**」をクリックします。
      * ルートパス：&lt;**/etc/designs/an-scf-sandbox** を参照します>
      * 「**完了**」をクリックします。
      * 「**フィルターを追加**」をクリックします。
      * ルートパス：&lt;**/content/an-scf-sandbox** を参照します>
      * 「**完了**」をクリックします。
   * 「**保存**」をクリックします。


* 「**ビルド**」をクリックします。

Now you can select **Download** to save it to disk and **Upload Package** elsewhere, as well as select **More > Replicate** in order to push the sandbox to a localhost publish instance to expand the realm of your sandbox.