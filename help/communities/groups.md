---
title: コミュニティグループコンソール
seo-title: コミュニティグループコンソール
description: グループコンソールにより、コミュニティグループを作成できます
seo-description: グループコンソールにより、コミュニティグループを作成できます
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# コミュニティグループコンソール {#community-groups-console}

The Groups console provides access to creating community groups when a community site&#39;s [template structure](/help/communities/sites-console.md#step1) includes the [groups function](/help/communities/functions.md#groups-function).

* AEM Communitiesでは、他のグループ内でのグループのネストをサポートしています。 グループの入れ子は、新しいグル [ープの構造に](/help/communities/tools-groups.md) groups関数が含まれる場合に可能です。
* 作成者環境の場合のみ、サイト作成ウィザードに似たグループ作成ウィザードがあります。
* コミュニティサイトの構造またはコミュニティグループの構造にグループ機能を追加する際に、メンバーが公開環境でグループを作成できるかどうかを設定できます。

Of the three group templates included, only the `Reference Group` template includes a groups function in its structure.

コミュニティグループの様々な側面は、次のとおりです。

* **作成**:新しいグループは、作成者に対しても、オプションで発行インスタンスに対しても作成できます。
* **制御**:グループは、オープンまたはシークレットのどちらでも構いません。
* **入れ子**:groupには、0個以上のグループを含めることができます。

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>This Groups console, only accessible from the Communities Sites console, is not to be confused with the member [Groups console](/help/communities/members.md) for managing member groups.
>
>メンバーグループは、パブリッシュ環境に登録されたユーザーグループであり、[トンネルサービス](/help/communities/deploy-communities.md#tunnel-service-on-author)を使用してオーサー環境からアクセスします。


## グループ作成 {#group-creation}

グループコンソールにアクセスするには：

* 作成者の場合、管理者権限でサインインします。
* From global navigation: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* 既存のコミュニティサイトフォルダを選択して開きます。
* フォルダ内のコミュニティサイトのインスタンスを選択します。

   * コミュニティサイトの構造には、グループ機能が含まれている必要があります。
   * These screen shots are from the Getting Started tutorial after [creating groups on publish](/help/communities/published-site.md).

* **グループフォルダー**&#x200B;を選択して、開きます。

   開いたら、オーサーまたはパブリッシュで作成されたすべての既存のグループが表示されます。

   このグループコンソールから、新しいグループを作成できます。

   ![chlimage_1-200](assets/chlimage_1-200.png)

* Select the **Create Group** button.

### 手順 1：コミュニティグループテンプレート {#step-community-group-template}

![多言語コミュニティグループ](assets/multi-lingual-group.png)

* **コミュニティグループのタイトル**

   グループの表示タイトル。
タイトルは、グループのパブリッシュされたサイトに表示されます。

* **コミュニティグループの説明**

   グループの説明です。

* **コミュニティグループのルート**

   グループのルートパス。
デフォルトのルートは親サイトですが、ルートはWebサイト内の任意の場所に移動できます。 変更することはお勧めしません。

* **[追加の利用可能なコミュニティグループの言語]メニュー**

   ドロップダウンを使用して、利用可能なコミュニティグループの言語を選択します。 このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。

* **コミュニティグループ名**

   URLに表示されるグループのルートページの名前。

   * 重複 — グループの作成後に簡単に変更されないので、名前を確認します。
   * ベースURLは、 `Community Group Name`
   * 有効なURLの場合は、「.html」を追加します。
      *例えば*、 `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **コミュニティグループテンプレート** メニュー

   ドロップダウンを使用して、利用可能なコミュニティグル [ープテンプレートを選択しま](/help/communities/tools.md)す。

### 手順 2：デザイン {#step-design}

### コミュニティグループのテーマ {#community-group-theme}

このフレームワークでは、レスポンシブで柔軟なサイトデザインを実現できるよう、[Twitter Bootstrap](https://twitterbootstrap.org/) を使用しています。プリロードされた多数のブートストラップテーマの1つを選択して、選択したコミュニティグループテンプレートのスタイルを設定するか、ブートストラップテーマをアップロードできます。

選択すると、テーマは不透明な青のチェックマークでオーバーレイされます。

親サイトのテーマとは異なるテーマを選択することもできます。

コミュニティサイトがパブリッシュされた後、[プロパティを編集](#modifyinggroupproperties)して、別のテーマを選択できます。

### コミュニティグループブランディング {#community-group-branding}

![chlimage_1-201](assets/chlimage_1-201.png)

コミュニティサイトブランディングとは、各ページ上部にヘッダーとして表示される画像のことです。他のサイトページとは異なるグループのバナーを表示できます。

画像の幅は、予想されるブラウザー内でのページの表示に合わせます。画像の高さは 120 ピクセルにします。

画像を選択するときは、次の点に注意してください。

* 画像の高さは、画像の上端から120ピクセルに切り抜かれます。
* 画像はブラウザーウィンドウの左端に固定されます
* 画像の幅が次のような場合、画像のサイズは変更されません。

   * ブラウザーの幅より小さい場合、画像は水平方向に繰り返されます。
   * ブラウザーの幅より大きい場合、画像は切り抜かれたように見えます。

### 手順 3：設定 {#step-settings}

**モデレート**

![コミュニティグループのメンバの役割を選択](assets/group-admin.png)

**コミュニティグループのモデレーター**

デフォルトで、親コミュニティサイトのモデレーターリストが継承されます。

グループに固有のモデレーターを追加できます。 メンバーを(投稿環境から)検索し、モデレーターとして追加

**グループ管理者**

デフォルトでは、親コミュニティサイト管理者もグループの管理者です。

ただし、独立したグループ管理者を割り当てることは可能です。 グループ管理者は、グループ（G1など）を管理し、G1の下にネストされたサブグループを作成できます。 さらに、サブグループに異なる管理者を割り当てることができます。

従って、ユーザU1は、グループG1の管理者であり、ネストされたグループG2の正規ユーザである可能性がある。

**メンバーシップ**

メンバーシップ設定によって、コミュニティグループをセキュリティ保護する 3 つの方法のうち 1 つを選択できます。

![chlimage_1-202](assets/chlimage_1-202.png)

* **オプションのメンバーシップ**

   選択した場合、コミュニティグループはパブリックグループです。 サイトメンバーは、明示的にグループに参加することなく、グループや投稿に参加できます。 デフォルトで選択されています。

* **必要なメンバーシップ**

   選択した場合、コミュニティグループは開いているグループです。 コミュニティサイトのメンバーは表示できますが、コンテンツを投稿するにはグループに参加する必要があります。 Members join by selecting the `Join` button in the publish environment. 初期設定では選択されていません。

* **制限されたメンバーシップ**

   選択した場合、コミュニティグループは秘密のグループです。 コミュニティのメンバーは明示的に招待する必要があります。 招待されたメンバーは検索ボックスに入力されます。 Members can be added later using the [Members and Groups consoles](/help/communities/members.md) the author environment. 初期設定では選択されていません。

**サムネイル**

![chlimage_1-203](assets/chlimage_1-203.png)

サムネイルは、オーサーおよびパブリッシュのグループに対して表示される画像です。

グループ画像の最適なサイズは、サポートされている画像形式（JPG や PNG など）の 170 x 90 ピクセルです。

画像を追加しない場合は、デフォルトの画像が表示されます。

![chlimage_1-204](assets/chlimage_1-204.png)

### 手順 4：グループの作成 {#step-create-group}

![chlimage_1-205](assets/chlimage_1-205.png)

調整が必要な場合は、「**戻る**」ボタンを使用して調整を行います。

Once **Create** is selected and started, the process of creating the group cannot be interrupted.

処理が完了すると、新しいサブコミュニティサイト（グループ）のカードがCommunitiesのサイトグループコンソールに表示され、作成者がページコンテンツを追加したり、管理者がサイトのプロパティを変更したりできます。

![コミュニティグループを作成する](assets/create-community-groups.png)

>[!NOTE]
>
>それぞれのコミュニティサイトのコミュニティグループコンソールに、[手順 1：コミュニティグループテンプレート](/help/communities/groups.md#step-community-group-template)の「追加の使用可能なコミュニティグループの言語」で指定したすべての言語でグループが作成されます。


## 作成者グループのコンテンツ {#author-group-content}

![chlimage_1-206](assets/chlimage_1-206.png)

グループのページコンテンツは、他のAEMページと同じツールを使用して作成できます。 オーサリング用にグループを開くには、グループカードの上にカーソルを置くと表示される「サイトを開く」アイコンを選択します。

## グループプロパティの変更 {#modify-group-properties}

コミュニティグループの作成プロセスで指定した既存のサブコミュニティサイトのプロパティは、グループカードの上にカーソルを置くと表示される「サイトを編集」アイコンを選択して変更できます。

![chlimage_1-207](assets/chlimage_1-207.png)

以下のプロパティの詳細は、[グループ作成](#group-creation)で説明した内容と同じです。ネストされたグループは、パブリッシュフォルダーで作成した場合でも、作成者環境で作成した場合でも、変更が可能です。

![chlimage_1-208](assets/chlimage_1-208.png)

### 基本事項の変更 {#modify-basic}

基本パネルでは、次のものを変更できます。

* コミュニティグループのタイトル
* コミュニティグループの説明

コミュニティグループ名は変更できません。

別のコミュニティグループテンプレートを選択しても、テンプレートとサイトの間に関係は残っていないので、既存のコミュニティグループサイトに影響が及ぶことはありません。

その一方で、サブコミュニティの[構造](#modify-structure)は変更できます。

### 構造の変更 {#modify-structure}

構造パネルでは、オーサー環境またはパブリッシュ環境でサブコミュニティを作成するときに選択したコミュニティグループテンプレートから最初に作成した構造を変更できます。パネルから、次の操作を行うことができます。

* Drag-and-drop additional [community functions](/help/communities/functions.md) into the site structure.
* サイト構造内のコミュニティ関数のインスタンスで、次の操作を行います。

   * **`Gear icon`**
表示タイトル、URL名*、権限を持つメンバー・グループなどの設 [定を編集します](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
サイト構造から関数を削除（削除）します。

   * **`Grid icon`**
サイトのトップレベルナビゲーションバーに表示される機能の順序を変更します。

>[!CAUTION]
>
>表示タイトルは副作用なしで変更できますが、コミュニティサイトに属するコミュニティ機能のURL名を編集することはお勧めしません。
>
>例えば、URL の名前を変更しても、既存の UGC は移動されません。そのため、UGC が「失われる」ことになります。


>[!CAUTION]
>
>The groups function must *not *be the *first nor the only* function in the site structure.
>
>他の機能（[ページ機能](/help/communities/functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。


**例：サブコミュニティ（グループ）構造へのカレンダー機能の追加**

![chlimage_1-209](assets/chlimage_1-209.png)

### デザインの変更 {#modify-design}

デザインパネルでは、次のものを変更できます。

* [コミュニティグループのテーマ](#community-group-theme)
* [コミュニティグループブランディング](#community-group-branding)

   * パネルの下部までスクロールして、ブランド画像を変更します。

### 設定の変更 {#modify-settings}

設定パネルでは、コミュニティの[モデレーター](#moderation)を追加できます。

### メンバーシップの変更 {#modify-membership}

[メンバーシップ](#membership)パネルは情報提供のみを目的としています。確立されたグループメンバーシップのタイプを、オプション、必須、制限のいずれでも変更することはできません。

### サムネイルの変更 {#modify-thumbnail}

[サムネイル](#thumbnail)パネルでは、コミュニティグループを表す画像をアップロードできます。この画像は、パブリッシュ環境でサイト訪問者に表示され、オーサー環境のコミュニティサイトのグループコンソールにも表示されます。

## グループの公開 {#publish-the-group}

![chlimage_1-210](assets/chlimage_1-210.png)

After a community group has been newly created or modified, it is possible to publish (activate) the group by selecting the `Publish Site` icon.

グループが正常に公開されると、メッセージが表示されます。

![chlimage_1-211](assets/chlimage_1-211.png)

>[!CAUTION]
>
>親コミュニティサイトおよび親グループが既に公開されている必要があります。
>
>コミュニティサイトおよびネストされたグループは、階層の上から下の順に公開される必要があります。


## グループの削除 {#delete-the-group}

![削除アイコン]()

コミュニティグループコンソール内のグループを削除するには、グループを削除アイコンを選択します。このアイコンは、グループにマウスポインターを置くと表示されます。

グループを削除すると、グループに関連付けられているアイテムはすべて削除されます。例えば、グループのコンテンツはすべて永久に削除され、ユーザーメンバーシップはシステムから削除されます。
