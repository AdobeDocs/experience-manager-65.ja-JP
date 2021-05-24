---
title: タグの管理
seo-title: タグの管理
description: AEM でタグを管理する方法について説明します。
seo-description: AEM でタグを管理する方法について説明します。
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 51%

---

# タグの管理 {#administering-tags}

タグは、Web サイト内のコンテンツをすばやく簡単に分類するために使用します。検索の結果としてコンテンツをよりすばやく見つけることのできるキーワードまたはラベル（メタデータ）と考えることができます。

Adobe Experience Manager（AEM）では、タグが以下のプロパティとなる場合があります。

* ページのコンテンツノード（[タグの使用](/help/sites-authoring/tags.md)を参照）。

* アセットのメタデータノード（[デジタルアセット用のメタデータの管理](/help/assets/metadata.md)を参照）。

ページやアセットに加え、AEM Communities の機能では次の場所でタグが使用されます。

* ユーザー生成コンテンツ（[UGC のタグ付け](/help/communities/tag-ugc.md)を参照）。

* イネーブルメントリソース（[イネーブルメントソースのタグ付け](/help/communities/functions.md#catalog-function)を参照）。

## タグの機能 {#tag-features}

AEM 内のタグには以下のような機能があります。

* タグは様々な名前空間にグループ分けできます。階層で分類を作成できます。この分類は、AEM 全体で使用されます。
* 新規に作成するタグの主な制限は、特定の名前空間内で一意でなければならないことです。
* タグのタイトルには、タグパスの区切り文字を含めないでください（含めても表示されません）。

   * colon `:` — 名前空間タグを区切る
   * フォワードスラッシュ`/` — サブタグを区切ります。

* タグは、作成者およびサイト訪問者が適用できます。すべてのフォームのタグは、作成者に関係なく、ページへの割り当て時および検索時に選択できるようになっています。
* タグの作成と分類の変更は、「tag-administrators」グループのメンバーと`/content/cq:tags`に対する変更権限を持つメンバーがおこなえます。

   * 子タグが含まれるタグはコンテナタグと呼ばれます
   * コンテナタグ以外のタグはリーフタグと呼ばれます
   * タグの名前空間はリーフタグかコンテナタグのいずれかです

* タグを[検索コンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html)で使用すると、コンテンツを簡単に検索できます。
* タグは [Teaser コンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)で使用され、ユーザーのタグクラウドを監視してターゲットのコンテンツを提供できます。
* タグ付けがコンテンツの重要な側面である場合は、次のことに注意します。

   * タグとタグを使用するページを必ずパッケージ化すること
   * [タグの権限](#setting-tag-permissions)に読み取りアクセスを有効にすること

## タグ付けコンソール {#tagging-console}

タグ付けコンソールは、タグと分類の作成および管理に使用します。1つの目的は、基本的に同じものに関連する多くの類似タグを持つのを避けることです。例えば、pageとpages、footwearとshoesなどです。

タグは、複数の名前空間にグループ分けして、新規のタグを作成する前に既存のタグの使用状況を確認し、現在参照されているコンテンツからタグを切り離すことなく整理し直すことによって管理します。

タグ付けコンソールにアクセスするには：

* オーサー環境で
* 管理者権限でサインインします
* グローバルナビゲーションから、次の操作をおこないます

   * **`Tools`**&#x200B;を選択します。
   * **`General`**&#x200B;を選択します。
   * **`Tagging`**&#x200B;を選択します。

![managing_tags_usingthetagasadministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 名前空間の作成 {#creating-a-namespace}

新しい名前空間を作成するには、「**`Create Namespace`**」アイコンを選択します。

名前空間はそれ自体がタグです。サブタグが含まれている必要はありません。ただし、分類の作成を続けるには、[サブタグ](#creating-tags)を作成します。これはリーフタグまたはコンテナタグになります。

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **タイトル**

   *（必須）* 名前空間の表示タイトル。

* **Name**
   *（オプション）* 名前空間の名前。指定しない場合、有効なノード名が「タイトル」から作成されます。[タグ ID](/help/sites-developing/framework.md#tagid) を参照してください。

* **説明**

   *（オプション）* 名前空間の説明。

必要な情報を入力したら

* 「**作成**」を選択します

### タグの操作  {#operations-on-tags}

名前空間または他のタグを選択すると、次の操作をおこなえるようになります。

* [プロパティを表示](#viewing-tag-properties)
* [参照](#showing-tag-references)
* [タグを作成](#creating-tags)
* [編集](#editing-tags)
* [移動](#moving-tags)
* [統合](#merging-tags)
* [公開](#publishing-tags)
* [非公開](#unpublishing-tags)
* [削除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

ブラウザーウィンドウの幅が狭く、すべてのアイコンが表示されない場合は、右端のアイコンが&#x200B;**`... More`**&#x200B;アイコンの下にグループ化され、選択すると非表示の操作アイコンのドロップダウンリストが表示されます。

![chlimage_1-185](assets/chlimage_1-185.png)

### 名前空間タグの選択 {#selecting-a-namespace-tag}

最初に選択したときに、名前空間にタグが含まれていない場合は右にプロパティが表示され、含まれている場合は子タグが表示されます。選択した各タグには、そのタグに含まれるタグか、子タグがない場合はそのプロパティが表示されます。

操作対象のタグを選択したり、複数選択をおこなう場合は、タイトルの横にあるアイコンを選択するだけです。タイトルを選択すると、プロパティのみが表示されるか、タグを開いてその内容を表示します。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### タグプロパティの表示 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

名前空間または他のタグが選択されている場合、**`View Properties`**&#x200B;アイコンを選択すると、`name`、最後に編集した時間、参照数に関する情報が表示されます。 公開された場合は、最後に公開された日時と公開者のIDが表示されます。 この情報は、タグ列の左側の列に表示されます。

![chlimage_1-189](assets/chlimage_1-189.png)

### タグ参照の表示 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

名前空間または他のタグが選択されているときに「**参照**」アイコンをクリックすると、そのタグが適用されているコンテンツが特定されます。

まず、適用されているタグの数が表示されます。

![chlimage_1-191](assets/chlimage_1-191.png)

数の右にある矢印を選択すると、参照名がリストされます。

参照の上にカーソルを重ねると、その参照へのパスがツールチップとして表示されます。

![chlimage_1-192](assets/chlimage_1-192.png)

### タグの作成 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

（タイトルの横にあるアイコンを選択して）名前空間または他のタグを選択すると、**`Create Tag`**&#x200B;アイコンを選択して、現在のタグの子タグを作成できます。

![chlimage_1-194](assets/chlimage_1-194.png)

* **タイトル**
*（必須） *タグの表示タイトル。

* **名前**
*（オプション） *タグの名前。指定しない場合、有効なノード名が「タイトル」から作成されます。[タグ ID](/help/sites-developing/framework.md#tagid) を参照してください。

* **説明**
*（オプション） *タグの説明。

必要な情報を入力したら

* 「**作成**」を選択します

### タグの編集  {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

名前空間または他のタグを選択した場合は、**`Edit`**アイコンを選択して、タイトルや説明を変更し、タイトルのローカライズを指定できます。

編集が完了したら、「**保存**」を選択します。

言語の翻訳の追加について詳しくは、[異なる言語でのタグの管理](#managing-tags-in-different-languages)の節を参照してください。

![chlimage_1-196](assets/chlimage_1-196.png)

### Moving Tags {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

名前空間または他のタグが選択されている場合、**`Move`**&#x200B;アイコンを選択すると、タグ管理者および開発者は、タグを新しい場所に移動したり、名前を変更したりして分類をクリーンアップできます。 選択したタグがコンテナタグの場合、タグを移動すると、すべての子タグも移動されます。

>[!NOTE]
>
>作成者はタグの[編集](#editing-tags)のみを許可し、タグの移動や名前変更は許可しないことをお勧めします。`title`

![chlimage_1-198](assets/chlimage_1-198.png)

* **パス**

   *（読み取り専用）* 選択したタグの現在のパス。

* **移動先** タグの移動先の新しいパスを参照します。

* **名前を**
変更最初に現在の 
`name`」と入力します。新しい`name`を入力できます。

* 「**保存**」を選択します

### タグの統合  {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

タグの統合は、分類が重複する場合に使用できます。タグ A がタグ B に統合されると、タグ A が付けられたすべてのページにタグ B が付けられ、作成者はタグ A を使用できなくなります。

名前空間または他のタグが選択されている場合、**結合**&#x200B;アイコンを選択するとパネルが開き、結合先のパスを選択できます。

![chlimage_1-200](assets/chlimage_1-200.png)

* **パス**

   *（読み取り専用）* 別のタグに結合するように選択されたタグのパス。

* **統合対象**&#x200B;統合先のタグのパスを参照して選択します。

>[!NOTE]
>
>統合すると、元から選択されていた&#x200B;**パス**&#x200B;は（実質的に）存在しなくなります。
>
>参照先のタグが移動または統合されても、タグは物理的には削除されないので、参照を維持することは可能です。

### タグの公開 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

名前空間または他のタグを選択したら、**公開**&#x200B;アイコンを選択して、パブリッシュ環境でタグをアクティブ化します。 ページのコンテンツと同様に、コンテナタグかどうかに関係なく、選択したタグのみが公開されます。

分類（名前空間とサブタグ）を公開するベストプラクティスとして、名前空間の[パッケージ](/help/sites-administering/package-manager.md)を作成します（[分類のルートノード](/help/sites-developing/framework.md#taxonomy-root-node)を参照）。パッケージを作成する前に、必ず名前空間に[権限](#setting-tag-permissions)を適用してください。

### タグを非公開にする {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

名前空間または他のタグが選択されている場合、**非公開**&#x200B;アイコンを選択すると、オーサー環境でタグが非アクティブ化され、パブリッシュ環境から削除されます。 `Delete`操作と同様に、選択したタグがコンテナタグの場合、オーサー環境ですべての子タグが非アクティブ化され、パブリッシュ環境から削除されます。

### タグの削除 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

名前空間または他のタグが選択されている場合、**削除**&#x200B;アイコンを選択すると、オーサー環境からタグが完全に削除されます。 タグが公開された場合は、パブリッシュ環境からも削除されます。 選択したタグがコンテナタグの場合、その子タグもすべて削除されます。

## タグの権限の設定 {#setting-tag-permissions}

タグの権限は、[&#39;secure（デフォルト）&#39;](/help/sites-administering/production-ready.md);タグに対して明示的に読み取り権限を許可する必要があるパブリッシュ環境向けのベストプラクティスです。 基本的には、オーサー環境で権限が設定された後にタグ名前空間のパッケージを作成し、すべてのパブリッシュインスタンスにパッケージをインストールします。

* オーサーインスタンスで

   * 管理者権限でサインインします
   * [セキュリティコンソール](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)にアクセスします

      * 例えば、http://localhost:4502/useradmin に移動します
   * 左側のウィンドウで、[読み取り権限](/help/sites-administering/security.md#permissions)を付与するグループ（またはユーザー）を選択します
   * 右側のウィンドウで、タグ名前空間への**パス**を見つけます。

      * 例： `/content/cq:tags/mycommunity`
   * **読み取り**&#x200B;列で`checkbox`を選択します。
   * 「**Save**」を選択します。



![chlimage_1-204](assets/chlimage_1-204.png)

* すべてのパブリッシュインスタンスが同じ権限となるようにします

   * 1 つのアプローチは、オーサー環境で名前空間の[パッケージを作成](/help/sites-administering/package-manager.md#package-manager)することです

      * `Advanced`タブで、`AC Handling`に`Overwrite`を選択します。
   * パッケージをレプリケートします

      * パッケージマネージャーから`Replicate`を選択します。


## Managing Tags in Different Languages {#managing-tags-in-different-languages}

タグの`title`プロパティは複数の言語に翻訳できます。 翻訳後は、ユーザーの言語またはページの言語に応じて適切なタグ`title`を表示できます。

### 複数言語でのタグタイトルの定義 {#defining-tag-titles-in-multiple-languages}

次に、タグ&#x200B;**Animals**&#x200B;の`title`を英語からドイツ語とフランス語に翻訳する方法を説明します。

まず、「**写真を保存**」名前空間の下のタグを選択し、「**`Edit`**」アイコンを選択します（[タグの編集](#editing-tags)の節を参照）。

タグを編集パネルで、タグのタイトルを翻訳する言語を選択できます。

各言語を選択すると、テキスト入力ボックスが表示され、翻訳されたタイトルを入力できます。

すべての翻訳を入力したら、「**保存**」を選択して編集モードを終了します。

![chlimage_1-205](assets/chlimage_1-205.png)

一般的に、タグに選択した言語はページの言語から取得されます。[`tag` ウィジェットが他のケース（フォームやダイアログなど）で使用されている場合、タグの言語はコンテキストによって変わります。](/help/sites-developing/building.md#tagging-on-the-client-side)

タグ付けコンソールでは、ページの言語設定の代わりに、ユーザーの言語設定が使用されます。タグ付けコンソールで、「Animals」タグに対して、ユーザープロパティで言語をフランス語に設定しているユーザーに対しては、「Animaux」が表示されます。

ダイアログに新しい言語を追加するには、[タグを編集ダイアログへの新しい言語の追加](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)を参照してください。

>[!NOTE]
>
>標準ページコンポーネントのタグクラウドとメタキーワードは、ページ言語に基づいてローカライズされたタグ`titles`を使用します（使用可能な場合）。

## リソース {#resources}

* [開発者向けタグ付け](/help/sites-developing/tags.md)

   タグ付けフレームワークに関する情報と、カスタムアプリケーションでタグを拡張および含める情報です。

* [クラシック UI のタグ付けコンソール](/help/sites-administering/classic-console.md)
