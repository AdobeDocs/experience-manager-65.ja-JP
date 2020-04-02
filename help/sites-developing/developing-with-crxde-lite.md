---
title: CRXDE Lite による開発
seo-title: CRXDE Lite による開発
description: CRXDE Lite は AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます
seo-description: CRXDE Lite は AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: 78133b41e1c99f8f86f4c0d51961287735423fe2

---


# CRXDE Lite による開発{#developing-with-crxde-lite}

ここでは、CRXDE Lite を使用して AEM アプリケーションを開発する方法について説明します。

使用可能な他の開発環境について詳しくは、概要のドキュメントを参照してください。

CRXDE Lite は AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Lite を使用すると、SVN によるログ記録や SVN との統合をおこなう間に、プロジェクトの作成や、ファイル（.jsp や .java など）、フォルダー、テンプレート、コンポーネント、ダイアログ、ノード、プロパティおよびバンドルの作成と編集を実行することができます。CRXDE Lite は、AEM サーバーに直接アクセスできない場合、すぐに使用可能なコンポーネントと Java バンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード補完および構文のハイライト表示を必要としない場合にお勧めします。

>[!NOTE]
>
>By default, all AEM users can access CRXDE Lite. If desired, [configure ACLs](/help/sites-administering/security.md#permissions-and-acls) for the following node so that only developers can access CRX DE Lite:
>
>`/libs/granite/crxde`

>[!NOTE]
>
>プロジェクトの開発時には [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) および [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) を使用することをお勧めします。

## CRXDE Lite の使用 {#getting-started-with-crxde-lite}

CRXDE Lite の使用を開始するには、次の手順に従ってください。

1. AEM をインストールします。
1. ブラウザで、と入力しま `https://<host>:<port>/crx/de`す。デフォルトでは、です `https://localhost:4502/crx/de`。
1. **ユーザー名**&#x200B;と&#x200B;**パスワード**&#x200B;を入力します。By default it is `admin` and `admin`.

1. 「**OK**」をクリックします。

ブラウザーでは、CRXDE Lite のユーザーインターフェイスは次のように表示されます。 

![chlimage_1-18](assets/chlimage_1-18.png)

これで、CRXDE Lite を使用してアプリケーションを開発できます。

## ユーザーインターフェイスの概要 {#overview-of-the-user-interface}

CRXDE Lite には以下の機能があります。

<table>
 <tbody>
  <tr>
   <td>上部のスイッチャーバー</td>
   <td>CRXDE Lite、パッケージマネージャー、パッケージ共有をすぐに切り替えることができます。</td>
  </tr>
  <tr>
   <td>ノードパスウィジェット</td>
   <td><p>現在選択しているノードのパスを表示します。</p> <p>このウィジェットに手動でパスを入力するか、または別の場所からパスを貼り付けて、Enter キーを押すと、特定のノードにジャンプできます。</p> <p>また、特定の名前を持つノードの検索がサポートされます。検索するノードの名前を入力して待機します（または、右側にある検索の記号をクリックします）。例えば、<em>oak</em> などの文字列をウィジェットに入力して、検索がどのように機能するかを確認できます。特定のノードがエクスプローラーウィンドウに読み込まれると、リストが表示されます。パスを選択して Enter キーを押すと、その場所に移動できます。この機能は、ブラウザーで現在 CRXDE クライアントアプリケーションに読み込まれているノードでしか使用できません。リポジトリ全体を検索する場合は、ツール／クエリを使用します。</p> </td>
  </tr>
  <tr>
   <td>エクスプローラーウィンドウ</td>
   <td><p>リポジトリ内のすべてのノードのツリーを表示します。</p> <p>ノードをクリックして、そのプロパティを「<strong>プロパティ</strong>」タブに表示します。ノードをクリックしたら、ツールバーでアクションを選択できます。ノード名を変更するには、ノードをもう一度クリックします。</p> <p>ツリーナビゲーションフィルター（双眼鏡アイコン）：リポジトリ内のノードのうち、入力テキストが名前に含まれているノードをフィルタリングできます。このフィルターは、ローカルに読み込まれたノードにのみ適用されます。<br /> </p> </td>
  </tr>
  <tr>
   <td>編集ウィンドウ</td>
   <td><p>「<strong>ホーム</strong>」タブ：コンテンツやドキュメントを検索したり、開発者リソース（ドキュメント、開発者向けブログ、ナレッジベース）とサポート（アドビのホームページとサポートセンター）にアクセスしたりできます。<br /> </p> <p><strong>エクスプローラー</strong>ウィンドウでファイルをダブルクリックして、その内容を表示します（例：.jsp ファイルまたは .java ファイル）。次に、ファイルを変更して保存できます。</p> <p><strong>編集</strong>ウィンドウでファイルを編集した後は、ツールバーで次のツールを使用できるようになります。<br /> </p> - <strong>ツリーに表示：</strong>リポジトリツリー内のファイルを表示します。<br /> - <strong>検索と置換</strong>：検索または置換をおこないます。<br /> <br /><strong>編集</strong>ウィンドウのステータス行をダブルクリックすると、<strong>行に移動</strong>ダイアログが開き、移動先の特定の行番号を入力できます。<br /> </td>
  </tr>
  <tr>
   <td>「プロパティ」タブ<br /> </td>
   <td>選択したノードのプロパティを表示します。新しいプロパティを追加したり、既存のプロパティを削除したりできます。<br /> </td>
  </tr>
  <tr>
   <td>「アクセス制御」タブ</td>
   <td><p>現在のパス、リポジトリレベルまたはプリンシパルに基づいて権限を表示します。</p> <p>権限は次のように分類されます。</p> <p>- <strong>適用可能なアクセス制御ポリシー</strong>：現在の選択項目に適用可能なポリシー。</p> <p>- <strong>ローカルアクセス制御ポリシー</strong>：現在の選択項目に対してローカルに適用される現在のポリシー。</p> <p>- <strong>有効なアクセス制御ポリシー</strong>：現在の選択項目に適用される現在のポリシーは、ローカルに設定されるか、親ノードから継承されます。</p> <p>注意：アクセス制御情報を確認できるようにするには、CRXDE Lite にログインしたユーザーに ACL エントリを読み取る権限が割り当てられている必要があります。デフォルトでは、匿名ユーザーはこの情報を確認できません。情報を確認するには、例えば admin としてログインしてください。</p> </td>
  </tr>
  <tr>
   <td>「レプリケーション」タブ</td>
   <td><p>現在のノードのレプリケーションステータスを表示します。現在のノードをレプリケーションできます。または削除をレプリケーションできます。</p> </td>
  </tr>
  <tr>
   <td>「コンソール」タブ<br /> </td>
   <td><p><strong>サーバーログ</strong>：</p> <p>ログメッセージを表示します。ログレベルの設定、コンソールのクリア、選択したスクロール位置での固定およびメッセージの表示の有効化／無効化をおこなうことができます。<br /> </p> <p><strong>バージョン管理</strong>:</p> <p>バージョン管理メッセージを表示します。<br /> </p> </td>
  </tr>
  <tr>
   <td>「ビルド情報」タブ<br /> </td>
   <td>バンドルのビルド中に情報を表示します。<br /> </td>
  </tr>
  <tr>
   <td>更新<br /> </td>
   <td>現在の選択項目を更新します。他のユーザーによる変更が、リポジトリの自分のビューで更新されます。自分がおこなった変更には影響を及ぼしません。<br /> </td>
  </tr>
  <tr>
   <td>すべて保存</td>
   <td><p><strong>すべて保存</strong>：<br /> </p> <p>おこなわれたすべての変更を保存します。「保存」をクリックするまで変更は一時的なものと見なされ、コンソールを終了すると失われます。</p> <p><strong>元に戻す</strong>:</p> <p>前回の保存アクションの後に、選択したノードに対しておこなった変更をすべて破棄し、選択したノード用にリポジトリの現在の状態を再読み込みします。</p> <p><strong>すべて元に戻す</strong>：</p> <p>前回の保存アクションの後に、リポジトリ全体でおこなった変更をすべて破棄し、リポジトリの現在の状態を再読み込みします。</p> </td>
  </tr>
  <tr>
   <td>作成 ...<br /> </td>
   <td><p>選択したノードの下に次の項目を作成するためのドロップダウンメニューです。<br /> </p> <p>- <strong>ノード</strong>：任意のノードタイプを持つノード<br /> </p> <p>- <strong>File</strong>: nt:file node and its nt:resource subnode</p> <p>- <strong>フォルダー</strong>：nt:folder ノード</p> <p>- <strong>テンプレート</strong>：AEM テンプレート</p> <p>- <strong>コンポーネント</strong>：AEM コンポーネント</p> <p>- <strong>ダイアログ</strong>：AEM ダイアログ</p> </td>
  </tr>
  <tr>
   <td>削除<br /> </td>
   <td>選択したノードを削除します。<br /> </td>
  </tr>
  <tr>
   <td>コピー</td>
   <td>選択したノードをコピーします。<br /> </td>
  </tr>
  <tr>
   <td>貼り付け<br /> </td>
   <td>Pastes the copied node under the selected node.<br /> </td>
  </tr>
  <tr>
   <td>移動 ...<br /> </td>
   <td>選択したノードを、ダイアログを使用して設定されたノードに移動します。</td>
  </tr>
  <tr>
   <td>名前を変更 ...<br /> </td>
   <td>選択したノードの名前を変更します。<br /> </td>
  </tr>
  <tr>
   <td>Mixin<br /> </td>
   <td>Mixin タイプをノードタイプに追加できます。ほとんどの場合、Mixin タイプは高度な機能（バージョン管理、アクセス制御、参照、ロックなど）をノードに追加するために使用されます。</td>
  </tr>
  <tr>
   <td>チーム<br /> </td>
   <td><p>標準のバージョン管理タスクを実行するためのドロップダウンメニューです。</p> <p>- SVN サーバーからリポジトリを<strong>更新する</strong></p> <p>- ローカルの変更を SVN サーバーに<strong>コミットする</strong></p> <p>- 現在のノードの<strong>ステータス</strong>を確認する</p> <p>- 現在のノードのサブツリーの<strong>再帰的なステータス</strong>を確認する</p> <p>- 作業用コピーを SVN サーバーから<strong>チェックアウトする</strong></p> <p>- SVN サーバーからプロジェクトを（作業用コピーを作成せずに）<strong>書き出す</strong></p> <p>- リポジトリから SVN サーバーにプロジェクトを<strong>読み込む<br /></strong> </p> <p>一部のタスクを実行できる十分な権限（特に、ローカルリポジトリに書き込む権限）を持つユーザーとしてログインする必要があります。<br /> </p> </td>
  </tr>
  <tr>
   <td>ツール<br /> </td>
   <td><p>次のツールを含むドロップダウンメニューです。</p> <p>- <strong>サーバー設定</strong>：Felix コンソールにアクセスします。</p> <p>- <strong>クエリ</strong>：リポジトリを照会します。</p> <p>- <strong>権限</strong>：権限管理を開いて、権限を確認および追加できます。</p> <p>- <strong>アクセス制御をテスト</strong>：特定のパスまたはプリンシパルに対する権限をテストできる場所です。</p> <p>- <strong>ノードタイプを書き出し</strong>：システム内のノードタイプを cnd 表記として書き出します。</p> <p>- <strong>ノードタイプを読み込み</strong>：cnd 表記を使用してノードタイプを読み込みます。</p> <p>- <strong>SiteCatalyst デバッガーをインストール</strong>：Analytics デバッガーをインストールする手順を示します。</p> </td>
  </tr>
  <tr>
   <td>ログインウィジェット<br /> </td>
   <td><p>現在ログイン中のユーザーとログイン先のワークスペースを表示します（例：admin@crx.default）。</p> <p>特定のユーザーとしてログインまたは再ログインするには、このウィジェットをクリックします。ログイン先のワークスペースを指定しない場合は、デフォルトのワークスペースである crx.default にログインします。</p> <p>匿名ユーザーとしてリポジトリを参照する場合は、ログイン名に <strong>anonymous</strong> を使用し、任意のパスワード（例：スペース、ドット）を使用します。<br /> </p> <p>承認が無効になった場合（期限切れの場合など）は、ログインウィジェットに「<strong>無許可 - ログイン</strong>」と表示されます。もう一度ログインするには、このメッセージをクリックします。</p> </td>
  </tr>
 </tbody>
</table>

## プロジェクトの作成 {#creating-a-project}

CRXDE Lite では、クリック 3 回で作業用プロジェクトを作成できます。The project wizard creates a new project under `/apps`, some content under `/conten`t and a package wrapping all the project the content under `/etc/packages`. リポジトリからプロパティをレンダリングし、Java クラスを呼び出して一部のテキストをレンダリングする jsp スクリプトを基に、作成したプロジェクトをすぐに使用して、**Hello World** を表示するサンプルページをレンダリングできます。

CRXDE Lite でプロジェクトを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションペインでノードを右クリックし、「 **作成…」を選択し**&#x200B;て、「プロジ **ェクトを作成…」を選択します。**.
注意：との下に新しいプロジェクトノードが設計上作成されているのと同じように、ツリーナビゲーションで任意のノードを右クリック `/apps,` でき `/content` ま `/etc/packages`す。

1. 以下を定義します。

   * **プロジェクト名** - プロジェクト名は、新しいノードとバンドルを作成するために使用します。例えば、`myproject` と指定します。

   * **Java パッケージ** - Java パッケージ名のプレフィックス（例：`com.mycompany`）です。

1. 「**作成**」をクリックします。
1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

**Hello World** を表示するサンプルページにアクセスするには、ブラウザーで次の URL を指定します。

`https://localhost:4502/content/<project-name>.html`

**Hello World** ページは、`sling:resourceType` プロパティを使用して jsp スクリプトを呼び出すコンテンツノードに基づいています。このスクリプトは、リポジトリから `jcr:title` プロパティを読み取り、プロジェクトバンドルで使用可能な SampleUtil クラスのメソッドを呼び出して本文のコンテンツを取得します。

以下のノードが作成されます。

* `/apps/<project-name>`:アプリケーションコンテナ。
* `/apps/<project-name>/components`:コンポーネントコンテナ。ページのレンダリングに使用するサンプルhtml.jspファイルを含みます。

* `/apps/<project-name>/src`:バンドルコンテナ。サンプルのプロジェクトバンドルが含まれます。

* `/apps/<project-name>/install`:コンパイル済みのバンドルコンテナ。コンパイル済みのサンプルプロジェクトバンドルが含まれます。
* `/content/<project-name>`:コンテンツコンテナ。
* /etc/packages/&lt;java-suffix>/&lt;project-name>.zip：プロジェクトのアプリケーションとコンテンツをすべてラップするパッケージです。このパッケージを使用して、追加のデプロイメント用（例：他の環境へのデプロイメント）またはパッケージ共有を使用した共有用のプロジェクトを再ビルドできます。

**myproject** という名前のプロジェクトと **mycompany** という Java パッケージのサフィックスを含む構造は、CRXDE Lite では次のように表示されます。

![chlimage_1-19](assets/chlimage_1-19.png)

![chlimage_1-20](assets/chlimage_1-20.png)

## フォルダーの作成 {#creating-a-folder}

CRXDE Lite でフォルダーを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. In the Navigation pane, right-click the folder under which you want to create the new folder, select **Create ...**, then **Create Folder ...**.

1. フォルダーの&#x200B;**名前**&#x200B;を入力して、「**OK**」をクリックします。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

## テンプレートの作成 {#creating-a-template}

CRXDE Lite でテンプレートを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、テンプレートを作成するフォルダーを右クリックして、「**作成**」、「**テンプレートを作成**」の順に選択します。

1. テンプレートの&#x200B;**ラベル**、**タイトル**、**説明**、**リソースタイプ**&#x200B;および&#x200B;**ランキング**&#x200B;を入力します。「**次へ**」をクリックします。

1. （オプション）「**許可されているパス**」を設定します。「**次へ**」をクリックします。

1. This step is optional: set the **Allowed Parents**. Click **Next**.

1. This step is optional: set the **Allowed Children**. Click **OK**.

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

次の項目が作成されます。

* A node of type `cq:Template` with Template properties

* ページコンテンツのプロパティを含む `cq:PageContent` タイプの子ノード

テンプレートにプロパティを追加できます。[プロパティの作成](#creating-a-property)の節を参照してください。

## コンポーネントの作成 {#creating-a-component}

ここで説明する機能を使用できるのは、CQ5 がインストールされている（つまり、ノードタイプ `cq:Component` をリポジトリで使用できる）場合のみです。

CRXDE Lite でコンポーネントを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、コンポーネントを作成するフォルダーを右クリックして、「**作成**」、「**コンポーネントを作成**」の順に選択します。

1. コンポーネントの&#x200B;**ラベル**、**タイトル**、**説明**、**スーパーリソースタイプ**&#x200B;および&#x200B;**グループ**&#x200B;を入力します。「**次へ**」をクリックします。

1. （オプション）コンポーネントのプロパティ（「**コンテナです**」、「**装飾なし**」、「**セル名**」、「**ダイアログパス**」）を設定します。「**次へ**」をクリックします。

1. （オプション）コンポーネントのプロパティ「**許可されている親**」を設定します。「**次へ**」をクリックします。

1. （オプション）コンポーネントのプロパティ「**許可されている子**」を設定します。「**OK**」をクリックします。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

次の項目が作成されます。

* A node of type `cq:Component`
* コンポーネントのプロパティ
* コンポーネントの .jsp スクリプト

## ダイアログの作成 {#creating-a-dialog}

CRXDE Lite でダイアログを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. In the Navigation pane, right-click the component where you want to create the dialog, select **Create ...**, then **Create Dialog ...**.

1. **ラベル**&#x200B;と&#x200B;**タイトル**&#x200B;を入力します。「**OK**」をクリックします。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

次の構造を持つダイアログが作成されます。

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

これで、プロパティを変更するか、または新しいノードを作成すれば、ニーズに合ったダイアログを作成できます。

ダイアログエディターを使用してダイアログを編集することもできます。CRXDE Lite でダイアログノードをダブルクリックすると、エディターが表示されます。ダイアログエディターについて詳しくは、[こちら](/help/sites-developing/dialog-editor.md)を参照してください。

## ノードの作成 {#creating-a-node}

CRXDE Lite でノードを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、新しいノードを作成するノードを右クリックして、「**作成**」、「**ノードを作成**」の順に選択します。
1. **名前**&#x200B;と&#x200B;**タイプ**&#x200B;を入力します。「**OK**」をクリックします。
1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

これで、プロパティを変更するか、または新しいノードを作成すれば、ニーズに合ったノードを作成できます。

>[!NOTE]
>
>ノードの作成を含むほとんどの編集操作では、すべての変更をメモリに保持し、保存時（「すべて保存」ボタンをクリックした場合）にのみそれらをリポジトリに格納します。ただし、移動などの一部の操作は自動的に保持されます。
>
>最初に変更を保存する際には、新しく作成したノードが親ノードのノードタイプで許可されるかどうかに関する検証も JCR リポジトリによって実行されます。ノードの保存時にエラーメッセージが表示された場合は、コンテンツ構造が有効かどうかを確認してください（例えば、`nt:unstructured` ノードを `nt:folder` ノードの子として作成することはできません）。

## プロパティの作成 {#creating-a-property}

CRXDE Lite でプロパティを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、新しいプロパティを追加するノードを選択します。
1. 下部のウィンドウの「**プロパティ**」タブで、「**名前**」、「**タイプ**」および「**値**」に入力します。「**追加**」をクリックします。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

## スクリプトの作成 {#creating-a-script}

新しいスクリプトを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、スクリプトを作成するコンポーネントを右クリックして、「**作成**」、「**ファイルを作成**」の順に選択します。

1. 拡張子を含む&#x200B;**ファイル名**&#x200B;を入力します。「**OK**」をクリックします。

1. 新しいファイルが編集ウィンドウ内のタブとして開きます。
1. ファイルを編集します。
1. 「**すべて保存**」をクリックして変更を保存します。

## バンドルの管理 {#managing-a-bundle}

CRXDE Lite では、OSGi バンドルの作成、OSGi バンドルへの Java クラスの追加および OSGi バンドルのビルドを簡単におこなうことができます。その後で、バンドルは OSGi コンテナに自動的にインストールされ、起動されます。

この節では、 `Test``HelloWorld`**Hello World!** をブラウザーに表示します。

### バンドルの作成 {#creating-a-bundle}

CRXDE Lite で Test バンドルを作成するには：

1. CRXDE Lite で、`myapp`プロジェクトウィザードを使用して [](#creating-a-project) プロジェクトを作成します。その他にも以下のノードが作成されます。

   * `/apps/myapp/src`
   * `/apps/myapp/install`

1. Right-click the folder `/apps/myapp/src` that will contain the `Test` bundle, select **Create ...**, then **Create Bundle ...**.

1. バンドルのプロパティを次のように設定します。

   * Symbolic Bundle Name: `com.mycompany.test.TestBundle`

   * バンドル名: `Test Bundle`
   * バンドルの説明：

      ```
      This is my Test Bundle
      ```

   * パッケージ:

      ```
      com.mycompany.test
      ```
   「**OK**」をクリックします。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

以下の要素がウィザードで作成されます。

* The node `com.mycompany.test.TestBundle` of type `nt:folder.` It is the bundle container node.

* The file `com.mycompany.test.TestBundle.bnd`. It acts as deployment descriptor for your bundle and consists of a set of headers.

* フォルダー構造は次のとおりです。

   * `src/main/java/com/mycompany/test` です。パッケージと Java クラスが格納されます。

   * `src/main/resources` です。バンドル内で使用されるリソースが格納されます。

* ファイ `Activator.java` ルです。 これは、バンドルの開始イベントと停止イベントが通知されるオプションのリスナークラスです。

次の表は、.bnd ファイルのすべてのプロパティと、その値および説明を示しています。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>値 （バンドルの作成時）<br /> </strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>Export-Package:</td>
   <td><p>*</p> <p>注意：この値は、バンドルの特異性を反映するように変更してください。</p> </td>
   <td>Export-Package ヘッダーは、バンドルから書き込まれるパッケージ（パッケージのコンマ区切りリスト）を定義します。書き込まれるパッケージは、バンドルの公開ビューを構成します。<br />
<br /> </td>
  </tr>
  <tr>
   <td>Import-Package:</td>
   <td><p>*</p> <p>注意：この値は、バンドルの特異性を反映するように変更してください。</p> </td>
   <td>Import-Package ヘッダーは、バンドル用に読み込むパッケージ（パッケージのコンマ区切りリスト）を定義します。</td>
  </tr>
  <tr>
   <td>Private-Package:</td>
   <td><p>*</p> <p>注意：この値は、バンドルの特異性を反映するように変更してください。</p> </td>
   <td>Private-Package ヘッダーは、バンドル用のプライベートパッケージ（パッケージのコンマ区切りリスト）を定義します。プライベートパッケージは内部実装を構成します。<br /> </td>
  </tr>
  <tr>
   <td>Bundle-Name:</td>
   <td>Test Bundle</td>
   <td>バンドルのわかりやすく簡単な名前を定義します。</td>
  </tr>
  <tr>
   <td>Bundle-Description:</td>
   <td>This is my Test Bundle</td>
   <td>バンドルのわかりやすく簡単な説明を定義します。</td>
  </tr>
  <tr>
   <td>Bundle-SymbolicName:</td>
   <td>com.mycompany.test.TestBundle</td>
   <td>バンドルのローカライズできない一意の名前を指定します。</td>
  </tr>
  <tr>
   <td>Bundle-Version:</td>
   <td>1.0.0-SNAPSHOT</td>
   <td>バンドルのバージョンを指定します。</td>
  </tr>
  <tr>
   <td>Bundle-Activator:</td>
   <td>com.mycompany.test.Activator</td>
   <td>バンドルの開始イベントと停止イベントが通知されるオプションのリスナークラスの名前を指定します。</td>
  </tr>
 </tbody>
</table>

bnd 形式について詳しくは、OSGi バンドルを作成するために CRXDE で使用される [bnd ユーティリティ](https://bndtools.org/)に関するページを参照してください。

### Java クラスの作成 {#creating-a-java-class}

Test バンドル内に `HelloWorld` Java クラスを作成するには：

1. ブラウザーで CRXDE Lite を開きます。
1. In the Navigation pane, right-click the node containing the `Activator.java` file ( `/apps/myapp/src/com.mycompany.test.TestBundle/src/main/java`), select **Create ...**, then **Create File ...**.

1. Name the file `HelloWorld.java`. 「**OK**」をクリックします。

1. `HelloWorld.java` ファイルが編集ウィンドウで開きます。
1. 次の行を `HelloWorld.java` に追加します。

   ```
     package com.mycompany.test;
   
     public class HelloWorld {
     public String getString(){
     return "Hello World!";
     }
     }
   ```

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

### バンドルのビルド {#building-a-bundle}

Test バンドルをビルドするには：

1. ブラウザーで CRXDE Lite を開きます。
1. ナビゲーションウィンドウで、.bnd ファイルを右クリックし、「**ツール**」、「**バンドル**」の順に選択します。

バンドルを作成ウィザードの役割を次に示します。

* Java クラスをコンパイルします。
* コンパイル済みの Java クラスとリソースを格納する .jar ファイルを作成して、`myapp/install` フォルダーに配置します。
* OSGi コンテナにバンドルをインストールして起動します。

Test バンドルの効果を確認するには、Java メソッド HelloWorld.getString() を使用するコンポーネントおよびそのコンポーネントによってレンダリングされるリソースを作成します。

1. コンポーネントを下に作 `mycomp` 成しま `myapp/components`す。

1. コード `mycomp.jsp` を編集し、次の行に置き換えます。

   ```
     <%@ page import="com.mycompany.test.HelloWorld"%><%
     %><%@ include file="/libs/foundation/global.jsp"%><%
     %><% HelloWorld hello = new HelloWorld();%><%
     %>
     <html>
     <body>
     <b><%= hello.getString() %></b><br>
     </body>
     </html>
   ```

1. Create the resource `test_node` of type `nt:unstructured` under `/content`.

1. For `test_node`, create the following property: Name = `sling:resourceType`, Type = `String`, Value = `myapp/components/mycomp`.

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

1. ブラウザーで、次をリクエストしま `test_node`す。 `https://<hostname>:<port>/content/test_node.html`.

1. **Hello World!** というメッセージと共にページが表示されます。

## ノードタイプの書き出しと読み込み {#exporting-and-importing-node-types}

With CRXDE Lite you can import and/or export node type definitions in [CND (Compact Namespace and Node Type Definition) notation](https://jackrabbit.apache.org/jcr/node-type-notation.html).

ノードタイプ定義を書き出すには：

1. ブラウザーで CRXDE Lite を開きます。
1. 必要なノードを選択します。
1. 「**ツール**」、「**ノードタイプを書き出し**」の順に選択します。

1. cnd 表記の定義がブラウザーに表示されます。必要に応じて情報を保存します。

ノードタイプ定義を読み込むには：

1. ブラウザーで CRXDE Lite を開きます。
1. 「**ツール**」、「**ノードタイプを読み込み**」の順に選択します。

1. テキストボックスに定義の CND 表記を入力します。
1. 既存の定義を更新する場合は、「**更新を許可**」を選択します。
1. 「**読み込み**」をクリックします。

## ログ {#logging}

With CRXDE Lite you can display the file `error.log` that is located on the file system at `<crx-install-dir>/crx-quickstart/server/logs` and filter it with the appropriate log level. 以下の手順を実行します。

1. ブラウザーで CRXDE Lite を開きます。
1. ウィンドウの下部にある「**コンソール**」タブの右側のドロップダウンメニューで、「**サーバーログ**」を選択します。

1. 「**停止**」アイコンをクリックして、メッセージを表示します。

以下の操作を実行できます。

* Adjust the log parameters in the Felix Console by clicking the **Logging Configurations** icon.
* **ブラシ**&#x200B;アイコンをクリックしてメッセージを消去します。
* **ピン**&#x200B;アイコンをクリックして、現在選択されている場所にメッセージを固定します。
* 「**停止**」アイコンをクリックしてメッセージの表示を有効または無効にします。

## アクセス制御 {#access-control}

>[!NOTE]
>
>詳しくは、[ユーザー、グループおよびアクセス権の管理](/help/sites-administering/user-group-ac-admin.md)を参照してください。
