---
title: ページテンプレート - 編集可能
description: 非開発者がテンプレートを作成および編集し、そこから作成されたページとの動的な接続を保持し、ページコンポーネントをより一般的にする、編集可能なテンプレートが導入されました。
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3224'
ht-degree: 43%

---

# ページテンプレート - 編集可能 {#page-templates-editable}

編集可能テンプレートは、次の用途に導入されました。

* 専門的な作成者が [テンプレートの作成と編集](/help/sites-authoring/templates.md).

   * このような専門的な作成者は、**テンプレート作成者**&#x200B;と呼ばれます。
   * テンプレート作成者は、`template-authors` グループのメンバーである必要があります。

* テンプレートから作成されたすべてのページとの動的な接続を保持するテンプレートを提供します。 これにより、テンプレートに対する変更がページ自体に反映されます。
* ページコンポーネントの汎用性を高め、コアページコンポーネントをカスタマイズなしで使用できるようにします。

編集可能なテンプレートを使用すると、ページを構成する要素がコンポーネント内で分離されます。 UI で必要なコンポーネントの組み合わせを設定することで、ページのバリエーションごとに新しいページコンポーネントを開発する必要がなくなります。

>[!NOTE]
>
>[静的テンプレート](/help/sites-developing/page-templates-static.md) は、も使用できます。

このドキュメントでは、

* 編集可能なテンプレートの作成の概要を説明します。

   * 詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)を参照してください。

* 編集可能なテンプレートの作成に必要な管理者/開発者のタスクについて説明します
* 編集可能なテンプレートの技術的基礎について説明します

このドキュメントでは、テンプレートの作成と編集について既に理解していることを前提としています。オーサリングに関するドキュメント[ページテンプレートの作成](/help/sites-authoring/templates.md)を参照してください。ここでは、テンプレート作成者に公開されている編集可能テンプレートの機能について詳しく説明されています。

>[!NOTE]
>
>次のチュートリアルは、新しいプロジェクトで編集可能なページテンプレートを設定する場合にも役立つ場合があります。
>[AEM Sites の概要（パート 2）- ベースページとテンプレートの作成](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=en)

## 新しいテンプレートの作成 {#creating-a-new-template}

編集可能なテンプレートの作成は、主に [テンプレートコンソールとテンプレートエディター](/help/sites-authoring/templates.md) テンプレート作成者が作成したもの。 ここでは、そのプロセスの概要を示し、技術的なレベルでどのような処理が行われるかを説明します。

AEMプロジェクトで編集可能なテンプレートを使用する方法について詳しくは、 [Lazybones を使用したAEMプロジェクトの作成](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478).

新しい編集可能テンプレートを作成する場合は、次の手順を実行します。

1. の作成 [テンプレート用のフォルダー](#template-folders). このフォルダーは必須ではありませんが、ベストプラクティスとして推奨されます。
1. を選択します。 [テンプレートタイプ](#template-type). このタイプは、 [テンプレート定義](#template-definitions).

   >[!NOTE]
   >
   >選択したテンプレートタイプが標準で提供されます。 また、 [独自のサイト固有のテンプレートタイプを作成する](/help/sites-developing/page-templates-editable.md#creating-template-types)（必要に応じて）

1. 新しいテンプレートの構造、コンテンツポリシー、初期コンテンツ、レイアウトを設定します。

   **構造**

   * 構造を使用して、テンプレートのコンポーネントとコンテンツを定義できます。
   * テンプレート構造で定義されたコンポーネントは、結果ページに移動することも、結果ページから削除することもできません。

      * テンプレートを `We.Retail` サンプルコンテンツ、基盤コンポーネントを選択するか、 [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja).
   * ページ作成者がコンポーネントを追加および削除できるようにするには、テンプレートに段落システムを追加します。
   * コンポーネントのロックを解除（再度ロックできます）して、初期コンテンツを定義できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)を参照してください。

   構造の技術的な詳細については、このドキュメントの[構造](/help/sites-developing/page-templates-editable.md#structure)を参照してください。

   **ポリシー**

   * コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。

      * 例えば、使用できるコンポーネントや最小／最大サイズを定義できます。
   * これらのポリシーは、テンプレート（およびテンプレートを使用して作成されたページ）に適用できます。

   テンプレート作成者がポリシーを定義する方法について詳しくは、 [ページテンプレートの作成](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   ポリシーの技術的な詳細については、 [コンテンツポリシー](/help/sites-developing/page-templates-editable.md#content-policies) 」を参照してください。

   **初期コンテンツ**

   * 初期コンテンツは、テンプレートに基づいてページが最初に作成されたときに表示されるコンテンツを定義します。
   * その後、ページ作成者が初期コンテンツを編集できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md#editing-a-template-initial-content-author)を参照してください。

   初期コンテンツの技術的な詳細については、 [初期コンテンツ](/help/sites-developing/page-templates-editable.md#initial-content) 」を参照してください。

   **レイアウト**

   * デバイスの形式に合わせてテンプレートのレイアウトを定義できます。
   * テンプレートがページオーサリングと同じように動作するには、レスポンシブレイアウトを使用します。

   テンプレート作成者がテンプレートレイアウトを定義する方法について詳しくは、 [ページテンプレートの作成](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   テンプレートのレイアウトの技術的な詳細については、 [レイアウト](/help/sites-developing/page-templates-editable.md#layout) 」を参照してください。

1. テンプレートを有効にして、特定のコンテンツツリーに対して許可します。

   * テンプレートを有効または無効にして、ページ作成者が使用できるようにしたり、使用できなくしたりできます。
   * テンプレートは、特定のページブランチに対して使用可能または使用不可にすることができます。

   テンプレート作成者によるテンプレートの有効化方法について詳しくは、 [ページテンプレートの作成](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   テンプレートの有効化の技術的な詳細については、このドキュメントの[使用するテンプレートの有効化と許可](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)を参照してください。

1. テンプレートを使用してコンテンツページを作成します。

   * テンプレートを使用してページを作成する場合、静的テンプレートと編集可能テンプレートの間に視覚的な違いはなく、表示上の違いもありません。
   * ページの作成者にとって、この処理は透過的です。

   ページ作成者がテンプレートを使用してページを作成する方法について詳しくは、[ページの作成と整理](/help/sites-authoring/managing-pages.md#templates)を参照してください。

   編集可能テンプレートを使用したページ作成の技術的な詳細については、このドキュメントの[作成されるコンテンツページ](/help/sites-developing/page-templates-editable.md#resultant-content-pages)を参照してください。

>[!TIP]
>
>国際化する必要がある情報は、テンプレートに含めないでください。 内部化の目的で、 [コアコンポーネントのローカライゼーション機能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=ja) をお勧めします。

>[!NOTE]
>
>テンプレートは、ページ作成ワークフローを効率化する強力なツールです。ただし、テンプレートが多すぎると作成者が圧倒され、ページ作成がを混乱するおそれがあります。経験上、テンプレートの数を 100 未満に抑えるのがよいでしょう。
>
>パフォーマンスに影響が及ぶ可能性があるので、1000 個を超えるテンプレートを用意することはお勧めしません。

>[!NOTE]
>
>エディタークライアントライブラリは、 `cq.shared` 名前空間（コンテンツページ内） 存在しない場合は、JavaScript エラーが発生します `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>すべてのサンプルコンテンツページには `cq.shared` が含まれているので、それらをベースとするコンテンツには自動的に `cq.shared` が含められます。ただし、サンプルコンテンツをベースとせず、ゼロから独自のコンテンツページを作成する場合は、`cq.shared` 名前空間を含める必要があります。
>
>詳しくは、[クライアントサイドライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

## テンプレートフォルダー {#template-folders}

以下のフォルダーを使用して、テンプレートを整理できます。

* **global**
* サイト固有：テンプレートを整理するために作成するサイト固有のフォルダーは、管理者権限を持つアカウントで作成されます。

>[!NOTE]
>
>フォルダーはネストできますが、**テンプレート**&#x200B;コンソールで表示すると、フラット構造として表されます。

標準のAEMインスタンスでは、 **global** テンプレートコンソールにフォルダーが存在します。 このフォルダーにはデフォルトのテンプレートが格納され、現在のフォルダーにポリシーやテンプレートタイプが見つからない場合にフォールバックとして機能します。 このフォルダーにデフォルトのテンプレートを追加するか、フォルダーを作成できます（推奨）。

>[!NOTE]
>
>カスタマイズしたテンプレートを格納するフォルダーを作成し、グローバルフォルダーは使用しないことをお勧めします。

>[!CAUTION]
>
>フォルダーは、`admin` 権限を持つユーザーが作成する必要があります。

テンプレートのタイプやポリシーは、次の優先順位に従ってすべてのフォルダーに継承されます。

1. 現在のフォルダー。
1. 現在のフォルダーの親。
1. `/conf/global`
1. `/apps`
1. `/libs`

許可されたすべてのエントリのリストが表示されます。オーバーラップする設定がある場合（`path`／`label`）、現在のフォルダーに最も近いインスタンスがユーザーに表示されます。

フォルダーを作成するには、次の手順を実行します。

* プログラムによる、またはCRXDE Lite
* 設定ブラウザーの使用

## CRXDE Lite の使用 {#using-crxde-lite}

1. インスタンスの新しいフォルダー（/conf の下）は、プログラムで自動的にまたは CRXDE Lite を使用して作成できます。

   次の構造を使用する必要があります。

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 次のプロパティをフォルダールートノードに定義できます。

   `<your-folder-name> [sling:Folder]`

   名前：`jcr:title`

   * 型：`String`

   * 値：**テンプレート**&#x200B;コンソールに表示される（フォルダーの）タイトルです。

1. In *追加* 標準のオーサリング権限 ( 例： `content-authors`)、グループを割り当て、作成者が新しいフォルダーにテンプレートを作成できるように、必要なアクセス権 (ACL) を定義します。

   この `template-authors` group は、割り当てが必要なデフォルトのグループです。 詳しくは、次の節[ACL とグループ](/help/sites-developing/page-templates-editable.md#acls-and-groups)を参照してください。

   アクセス権限の管理および割り当てについて詳しくは、[アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)を参照してください。

### 設定ブラウザーの使用 {#using-the-configuration-browser}

1. **グローバルナビゲーション**／**ツール**／**設定ブラウザー**&#x200B;に移動します。

   **グローバル**&#x200B;フォルダーを含めた既存のフォルダーは左側に一覧表示されます。

1. 「**作成**」をクリックします。
1. 内 **設定を作成** ダイアログで、次のフィールドを設定する必要があります。

   * **タイトル**:設定フォルダーのタイトルを指定します
   * **編集可能なテンプレート**:このフォルダー内で編集可能なテンプレートを許可する場合に選択します

1. クリック **作成**

>[!NOTE]
>
>設定ブラウザーで、グローバルフォルダーを編集し、 **編集可能なテンプレート** オプションを使用します。 ただし、この方法は推奨されるベストプラクティスではありません。
>
>詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

### ACL とグループ {#acls-and-groups}

（CRXDE を使用するか設定ブラウザーを使用して）テンプレートフォルダーを作成した後、セキュリティを確保するために、テンプレートフォルダーの適切なグループに ACL を定義する必要があります。

のテンプレートフォルダー [`We.Retail` 参照実装](/help/sites-developing/we-retail.md) は、例として使用できます。

#### template-authors グループ {#the-template-authors-group}

`template-authors` グループは、テンプレートへのアクセスを管理するために使用されるグループで、AEM に標準で付属していますが空です。ユーザーは、プロジェクト／サイトのグループに追加する必要があります。

>[!CAUTION]
>
>この `template-authors` グループが *のみ* テンプレートを作成する必要があるユーザー向けの機能です。
>
>テンプレートの編集は強力です。正しくおこなわないと、既存のテンプレートが壊れる場合があります。 したがって、この役割は重点的に設定し、適格なユーザーのみを含める必要があります。

次の表に、テンプレートの編集に必要な権限を示します。

<table>
 <tbody>
  <tr>
   <th>パス</th>
   <th>ロール／グループ</th>
   <th>権限<br /> </th>
   <th>説明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>テンプレート作成者<br /> </td>
   <td>読み込み、書き込み、レプリケート</td>
   <td>テンプレート作成者は、以下の場所でテンプレートを作成、読み取り、更新、削除、および複製します サイト固有 <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にテンプレートを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>replicateContent 作成者は、ページをアクティブ化する際に、ページのテンプレートをアクティブ化する必要があります</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>読み込み、書き込み、レプリケート</td>
   <td>テンプレート作成者は、以下の場所でテンプレートを作成、読み取り、更新、削除、および複製します サイト固有 <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にポリシーを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>コンテンツ作成者は、ページをアクティブ化する際に、ページのテンプレートのポリシーをアクティブ化する必要があります</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>テンプレート作成者</td>
   <td>読み取り</td>
   <td>テンプレート作成者は、事前定義済みのテンプレートタイプの 1 つに基づいてテンプレートを作成します。</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>なし</td>
   <td>匿名 Web ユーザーはテンプレートの種類にアクセスできません</td>
  </tr>
 </tbody>
</table>

デフォルトの `template-authors` グループは、プロジェクト設定のみに対応しています。この場合、`template-authors` のすべてのメンバーは、すべてのテンプレートへのアクセスとそれらの作成が許可されています。より複雑な設定では、複数のテンプレート作成者グループでテンプレートへのアクセスを分離する必要がある場合、より多くのカスタムテンプレート作成者グループを作成する必要があります。 ただし、テンプレート作成者グループの権限は同じです。

#### /conf/global の下の従来のテンプレート {#legacy-templates-under-conf-global}

テンプレートをに保存しない `/conf/global`. ただし、一部のレガシーインストールでは、この場所にテンプレートが存在する場合があります。 *のみ* このようなレガシーな状況では、次のような場合が考えられます `/conf/global` パスを明示的に設定します。

<table>
 <tbody>
  <tr>
   <th>パス</th>
   <th>ロール／グループ</th>
   <th>権限<br /> </th>
   <th>説明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>テンプレート作成者</td>
   <td>読み込み、書き込み、レプリケート</td>
   <td>テンプレート作成者は、以下の場所でテンプレートを作成、読み取り、更新、削除、および複製します <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にテンプレートを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>コンテンツ作成者は、ページをアクティベートする際に、ページのテンプレートをアクティベートする必要があります</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>読み込み、書き込み、レプリケート</td>
   <td>テンプレート作成者は、以下の場所でテンプレートを作成、読み取り、更新、削除、および複製します <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にポリシーを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>コンテンツ作成者は、ページをアクティブ化する際に、ページのテンプレートのポリシーをアクティブ化する必要があります</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>テンプレート作成者</td>
   <td>読み取り</td>
   <td>テンプレート作成者は、事前定義済みのテンプレートタイプの 1 つに基づいてテンプレートを作成します</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>なし</td>
   <td>匿名 Web ユーザーはテンプレートの種類にアクセスできません</td>
  </tr>
 </tbody>
</table>

## テンプレートタイプ {#template-type}

テンプレートを作成する際に、テンプレートタイプを指定します。

* テンプレートタイプは、テンプレートのテンプレートを効果的に提供します。 テンプレートを作成する際、選択したテンプレートタイプの構造と初期コンテンツを使用してテンプレートが作成されます。

   * テンプレートタイプがコピーされて、テンプレートが作成されます。
   * コピーが実行されると、テンプレートとテンプレートタイプの間の接続は、情報を提供するための静的参照のみになります。

* テンプレートタイプを使用して、次の項目を定義できます。

   * ページコンポーネントのリソースタイプ。
   * ルートノードのポリシー。テンプレートエディターで許可されるコンポーネントを定義します。
   * Adobeでは、テンプレートタイプで、モバイルエミュレーターのレスポンシブグリッドと設定のブレークポイントを定義することをお勧めします。 この手順はオプションです。これは、設定を個々のテンプレートで定義することもできるからです ( [テンプレートタイプとモバイルデバイスグループ](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)) をクリックします。

* AEM には、既製のテンプレートタイプがいくつか用意されています（HTML 5 ページ、アダプティブフォームページなど）。

   * その他の例は、 [`We.Retail`](/help/sites-developing/we-retail.md) サンプルコンテンツ。

* テンプレートタイプは、通常、開発者が定義します。

既製のテンプレートタイプは次のフォルダーに保存されています。

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>内の設定を変更しない `/libs` パス。 理由は、 `/libs` は、インスタンスを次回アップグレードするとき（ホットフィックスまたは機能パックを適用すると上書きされる場合があります）に上書きされます。

サイト固有のテンプレートタイプは、以下に相当する場所に保存してください。

* `/apps/settings/wcm/template-types`

カスタマイズしたテンプレートタイプの定義は、ユーザー定義フォルダー（推奨）または `global` フォルダーに保存してください。次に例を示します。

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>テンプレートタイプは、正しいフォルダー構造 ( つまり、 `/settings/wcm/...`) が含まれていない場合、テンプレートタイプが見つかりません。

### テンプレートタイプとモバイルデバイスグループ {#template-type-and-mobile-device-groups-br}

編集可能テンプレートで使用される[デバイスグループ](/help/sites-developing/mobile.md#device-groups)（プロパティ `cq:deviceGroups` の相対パスとして設定）によって、ページオーサリングの[レイアウトモード](/help/sites-authoring/responsive-layout.md)のエミュレーターとして利用できるモバイルデバイスが決まります。この値は次の 2 つの場所で設定できます。

* 編集可能テンプレートのタイプ
* 編集可能テンプレート上

新しい編集可能テンプレートを作成する場合、値はテンプレートタイプから個々のテンプレートにコピーされます。 値がタイプに設定されていない場合、テンプレートに設定できます。 テンプレートの作成後に、タイプからテンプレートに継承されることはありません。

>[!CAUTION]
>
>`cq:deviceGroups` の値は、`/etc/mobile/groups/responsive` などの絶対パスとしてではなく、`mobile/groups/responsive` などの相対パスとして設定する必要があります。

>[!NOTE]
>
>[静的テンプレート](/help/sites-developing/page-templates-static.md)では、`cq:deviceGroups` の値はサイトのルートに設定できます。
>
>編集可能テンプレートでは、この値はテンプレートレベルで保管されるようになっており、ページのルートレベルではサポートされません。

### テンプレートタイプの作成 {#creating-template-types}

他のテンプレートの基盤となるテンプレートを作成した場合、このテンプレートをテンプレートタイプとしてコピーできます。

1. 編集可能なテンプレートと同様に、テンプレートを作成します [ここに記載されているように](/help/sites-authoring/templates.md#creating-a-new-template-template-author)は、テンプレートタイプの基礎として使用できます。
1. CRXDE Liteを使用して、新しく作成したテンプレートを `templates` ノードから `template-types` ノードの [テンプレートフォルダー](/help/sites-developing/page-templates-editable.md#template-folders).
1. このテンプレートを[テンプレートフォルダー](/help/sites-developing/page-templates-editable.md#template-folders)の下の `templates` ノードから削除します。
1. `template-types` ノードの下にあるテンプレートのコピーで、すべての `jcr:content` ノードから `cq:template` および `cq:templateType` プロパティをすべて削除します。

また、GitHub で入手できる、編集可能テンプレートのサンプルを基盤として使用し、独自のテンプレートタイプを作成することもできます。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-sites-example-custom-template-type プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* プロジェクトを [ZIP ファイル](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)としてダウンロードします

## テンプレート定義 {#template-definitions}

編集可能テンプレートの定義は、[ユーザー定義フォルダー](/help/sites-developing/page-templates-editable.md#template-folders)（推奨）または `global` フォルダーに格納されます。次に例を示します。

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

テンプレートのルートノードは、以下のスケルトン構造を持つ `cq:Template` タイプです。

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主な要素は以下のとおりです。

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

このノードは、テンプレートのプロパティを保持します。

* **名前**：`jcr:title`

* **名前**：`status`

   * **型**：`String`

   * **値**: `draft`, `enabled`または `disabled`

### 構造 {#structure}

作成されるページの構造を定義します。

* 初期コンテンツ ( `/initial`) をクリックします。
* 構造に加えた変更は、そのテンプレートで作成されたすべてのページに反映されます。
* この `root` ( `structure/jcr:content/root`) ノードは、作成されたページで使用できるコンポーネントのリストを定義します。

   * テンプレート構造で定義されたコンポーネントは、作成されたページで移動することも、作成されたページから削除することもできません。
   * コンポーネントをロック解除すると、 `editable` プロパティをに設定します。 `true`.

   * 既にコンテンツを含むコンポーネントをロック解除すると、そのコンテンツは `initial` 分岐。

* `cq:responsive` ノードは、レスポンシブレイアウトの定義を保持します。

### 初期コンテンツ {#initial-content}

作成時に新しいページに含まれる初期コンテンツを定義します。

* すべての新しいページにコピーされる `jcr:content` ノードが含まれます。
* 構造 ( `/structure`) をクリックします。
* 作成後に初期コンテンツが変更されると、既存のページはすべて更新されます。
* この `root` ノードは、作成されたページで使用可能なコンポーネントを定義する、コンポーネントのリストを保持します。
* 構造モードでコンテンツをコンポーネントに追加し、後でそのコンポーネントのロックを解除（または逆）すると、このコンテンツが初期コンテンツとして使用されます。

### レイアウト {#layout}

条件 [テンプレートを編集すると、レイアウトを定義できます](/help/sites-authoring/templates.md)、このプラクティスでは [標準レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md) これは、 [設定済み](/help/sites-administering/configuring-responsive-layout.md).

### コンテンツポリシー {#content-policies}

コンテンツ（またはデザイン）ポリシーは、コンポーネントの使用可否や最小/最大の寸法など、コンポーネントのデザインプロパティを定義します。 これらのポリシーは、テンプレート（およびテンプレートを使用して作成されたページ）に適用できます。 コンテンツポリシーは、テンプレートエディターで作成および選択できます。

* `root` ノード上の `cq:policy` プロパティ
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
ページの段落システムのコンテンツポリシーに対する相対参照を提供します。

* `root` の下のコンポーネントを明示的に示すノードの `cq:policy` プロパティは、個々のコンポーネントのポリシーへのリンクを提供します。

* 実際のポリシー定義は、次の場所に保存されます。
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>ポリシー定義のパスは、コンポーネントのパスによって異なります。 この `cq:policy` は、設定自体への相対参照を保持します。

>[!NOTE]
>
>編集可能テンプレートから作成されたページの場合は、ページエディターでデザインモードが提供されません。
>
>編集可能テンプレートの `policies` ツリーは、次の場所にある静的テンプレートのデザインモード設定と同じ階層を持ちます。
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>静的テンプレートのデザインモード設定は、ページコンポーネントごとに定義されました。

### ページポリシー {#page-policies}

ページポリシーを使用すると、 [コンテンツポリシー](#content-policies) （メイン parsys）ページの場合は、テンプレートまたは結果ページのいずれか。

### テンプレートの使用の有効化と許可 {#enabling-and-allowing-a-template-for-use}

1. **テンプレートの有効化**

   テンプレートを使用する前に、次のいずれかの方法で有効にする必要があります。

   * [テンプレートの有効化](/help/sites-authoring/templates.md#enablingatemplateauthor) から **テンプレート** コンソール。

   * `jcr:content` ノードの status プロパティを設定する。

      * 例：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * プロパティを定義します。

         * 名前：ステータス
         * タイプ：String
         * 値：`enabled`

1. **許可されたテンプレート**

   * [許可されたテンプレートのパスを **ページプロパティ**](/help/sites-authoring/templates.md#allowing-a-template-author) サブブランチの適切なページまたはルートページの 1 つ。
   * プロパティを設定します。
      `cq:allowedTemplates` 
を 
必要なブランチの `jcr:content` ノードに設定します。
   例えば、次の値を使用します。

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 作成されるコンテンツページ {#resultant-content-pages}

編集可能テンプレートから作成されるページには、次の特徴があります。

* テンプレートの `structure` と `initial` を統合したサブツリーを使用して作成されます。

* テンプレートおよびテンプレートタイプに保持されている情報への参照を保持します。この機能は、 `jcr:content` ノードに次のプロパティを追加します。

   * `cq:template`
実際のテンプレートへの動的参照を提供します。テンプレートへの変更を実際のページに反映させることができます。

   * `cq:templateType`
テンプレートタイプへの参照を提供します。

![chlimage_1-71](assets/chlimage_1-71.png)

上の図は、テンプレート、コンテンツおよびコンポーネントの相関関係を示したものです。

* コントローラー - `/content/<my-site>/<my-page>`
テンプレートを参照した結果のページ。コンテンツがプロセス全体を制御します。定義に従って、適切なテンプレートとコンポーネントにアクセスします。

* 設定 - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
[テンプレートおよび関連するコンテンツポリシー](#template-definitions)がページ設定を定義します。

* モデル - OSGi バンドル
[OSGi バンドル](/help/sites-deploying/osgi-configuration-settings.md)が機能を実装します。

* 表示 — `/apps/<my-site>/components`
オーサー環境とパブリッシュ環境の両方で、コンテンツは [コンポーネント](/help/sites-developing/components.md).

ページをレンダリングする際の動作：

* **テンプレート**:

   * この `cq:template` 財産 `jcr:content` ノードが参照され、そのページに対応するテンプレートにアクセスできます。

* **コンポーネント**:

   * ページコンポーネントは、 `structure/jcr:content` テンプレートのツリーに `jcr:content` ページのツリー。

   * ページコンポーネントを使用すると、作成者は、「編集可能」のフラグが設定されたテンプレート構造のノード（およびその他の子）の編集のみ可能になります。
   * ページ上にコンポーネントをレンダリングすると、そのコンポーネントの相対パスは `jcr:content` ノード；下の同じ道 `policies/jcr:content` 次に、テンプレートのノードが検索されます。

      * この `cq:policy` このノードのプロパティは、実際のコンテンツポリシーを指します（つまり、このプロパティは、そのコンポーネントのデザイン設定を保持しています）。

      * この機能を使用すると、同じコンテンツポリシー設定を再利用する複数のテンプレートを作成できます。
