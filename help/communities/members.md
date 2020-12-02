---
title: メンバーコンソールとグループ管理コンソール
seo-title: メンバーコンソールとグループ管理コンソール
description: メンバーコンソールとグループ管理コンソールにアクセスする方法
seo-description: メンバーコンソールとグループ管理コンソールにアクセスする方法
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 36%

---


# メンバーコンソールとグループ管理コンソール  {#members-groups-management-consoles}

## 概要 {#overview}

AEM Communities の機能の多くは、サイト訪問者に対して、パブリッシュ環境でコミュニティに参加する前に登録とサインインを求めます。ユーザー登録は発行環境にのみ存在する必要があり、一般に&#x200B;*メンバー*&#x200B;と呼ばれ、作成者環境に登録された&#x200B;*ユーザー*&#x200B;と区別します。

### パブリッシュ環境のメンバー（ユーザー） {#members-users-on-publish}

Communitiesのメンバーとグループのコンソールを使用して、*publish*&#x200B;環境に登録されたメンバーとメンバーグループを&#x200B;*author*&#x200B;環境から作成し、管理できます。 これは[トンネルサービス](deploy-communities.md#tunnel-service-on-author)が有効な場合にのみ可能です。

### オーサー環境のユーザー {#users-on-author}

*author*&#x200B;環境に登録されたユーザーとグループを管理するには、プラットフォームのセキュリティコンソールを使用する必要があります。

* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL ユーザー]**&#x200B;を選択します。
* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL グループ]**&#x200B;を選択します。

>[!NOTE]
>
>サンプルコンテンツがデプロイされて有効になっていると、オーサー環境とパブリッシュ環境の両方に多数のサンプルユーザーが存在します。[nosamplecontent runmode](../../help/sites-administering/production-ready.md)で実行する場合、これらのユーザーは存在しません。

## メンバーコンソール {#members-console}

パブリッシュ環境で登録されたメンバーをオーサー環境で管理するには、次の場所にあるメンバーコンソールを使用します。

* グローバルナビゲーションから、**[!UICONTROL ナビゲーション]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL メンバー]**&#x200B;を選択します。

>[!CAUTION]
>
>[tunnel service](deploy-communities.md#tunnel-service-on-author)が有効になっていない場合は、Membersコンソールを使用できません。

![member-console1](assets/member-console1.png)

### 検索 {#search-features}

`Members`ヘッダーの左側にあるサイドパネルアイコンを選択して、検索サイドパネルを開きます。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

`Members`ヘッダーの左側にある検索アイコンを選択すると、検索側パネルが閉じられた状態に切り替わります。

### メンバーの統計 {#member-statistics}

`Views`、`Posts`、`Follows`、`Likes`の各列は、Adobe Analytics[が有効](sites-console.md#analytics)で、1つ以上のコミュニティサイトのメンバーである場合に更新されます。

### CSV の書き出し {#export-csv}

`Export CSV`リンクを選択すると、すべてのメンバーがコンマ区切り値のリストとしてダウンロードされ、スプレッドシートへのインポートに適しています。

列ヘッダーは次のとおりです。

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 新しいメンバーを作成 {#create-new-member}

公開環境にユーザを作成するには、`Create Member`を選択します。

![create-member1](assets/create-member1.png)

### 一般 - メンバー詳細 {#general-member-details}

大部分のフィールドはオプションです。メンバーは後からフィールドに自分のプロファイルを入力できます。

* **[!UICONTROL ID]**

（*必須*）許可可能なIDは、メンバーのログインIDです。
デフォルトでは、ID は必須の電子メールアドレスの値に設定されています。*IDは作成後は変更できません*。

* **[!UICONTROL 電子メールアドレス]**

（*必須*）メンバーの電子メールアドレス。
会員はプロファイルを更新する際に、自分のメールアドレスを変更することができます。
IDがデフォルトで電子メールアドレスに設定されている場合、電子メールアドレスが変更されても、IDは**&#x200B;変更されません。

* **[!UICONTROL パスワード]**

   （*必須*）サインインパスワード。

* **[!UICONTROL パスワードの確認入力]**

   （*必須*）確認のためにパスワードを再入力します。

* **[!UICONTROL メンバーをサイトに追加]**

   （*オプション*）既存のコミュニティサイトからメンバを選択して、コミュニティサイトのメンバグループに追加します。

* **[!UICONTROL メンバーをグループに追加]**

   （*オプション*）既存のメンバーグループから選択して、そのグループにメンバーを追加します。

* **[!UICONTROL 保存]**&#x200B;を選択

### 一般 - アカウント設定 {#general-account-settings}

アカウントの設定では、コミュニティ管理者は次のことができます。

* **[!UICONTROL ステータス]**
   * 禁止
メンバーがサインインできないため、ページを表示できないか、ログインが必要なアクティビティに参加できません。 未だにオープンコミュニティサイトを匿名で訪問している可能性がある。

   * 禁止されていないメンバーはコミュニティサイトのすべての機能にアクセスできます。

   デフォルトは `Not Banned` です。

* **[!UICONTROL 貢献度の制限]**

   オンにすると、メンバーがコンテンツを投稿する権限が制限されます。
初期設定は、貢献度の制限の設定によって異なります。[メンバーの貢献度の制限](limits.md)を参照してください。

* **[!UICONTROL パスワードを変更]**

   既存のメンバーの変更時に存在するリンク。 コミュニティ管理者がメンバーのパスワードをリセットする機能を提供します。

### 一般 - 写真 {#general-photo}

メンバーのアバターを設定するには、まず「**[!UICONTROL 画像をアップロード]**」を選択して、.jpg、.png、.tif、.gif のいずれかから画像の種類を選択します。画像の推奨されるサイズは、240 x 240ピクセル、72 dpiです。

### 一般 - メンバーをサイトに追加 {#general-add-member-to-sites}

1 つ以上のコミュニティサイトのメンバーグループにメンバーを追加できます。まず、テキストボックスにテキストを入力します。

### 一般 - メンバーをグループに追加 {#general-add-member-to-groups}

1 つ以上のメンバーグループにメンバーを追加できます。まず、テキストボックスにテキストを入力します。

### 「バッジ」タブ{#badges-tab}

`BADGES`パネルでは、手動でバッジを割り当てたり、取り消したりできます。 バッジは通常、獲得するものですが、役割の割り当てに使用することもできます。

[スコアとバッジ](implementing-scoring.md)も参照してください。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 追加バッジ]**
   * [使用可能なバッジ](badges.md)から選択するには、入力を開始します。 バッジを選択したら、各サイトまたはすべてのサイトを選択します。このサイト上に、会員のアバターと共にバッジを表示します。
   * 複数のバッジとサイトを選択できます。
* **[!UICONTROL バッジを削除]**
   * バッジの横にあるごみ箱アイコンを選択して、削除します。

## グループコンソール {#groups-console}

グループコンソールはオーサー環境から使用でき、パブリッシュ環境で登録されたメンバーグループの作成や管理をおこなうことができます。特に、以下の目的で使用されます。
* [特権を持つメンバーグループ](users.md#privilegedmembersgroups)
* [有効化リソース](resources.md)のグループベースの割り当て

グループコンソールにアクセスするには：
* グローバルナビゲーションから、**[!UICONTROL ナビゲーション]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL グループ]**&#x200B;を選択します。

>[!CAUTION]
>
>[トンネルサービス](deploy-communities.md#tunnel-service-on-author)が有効でない場合、グループコンソールを使用することはできません。

### 新しいグループを作成 {#create-new-group}

公開環境にグループを作成するには、`Add Group`を選択します。

![group-console1](assets/group-console1.png)

パブリッシュ側の新しいメンバーグループを作成するには、以下のフィールドを指定します。

* **[!UICONTROL ID]**

   （*必須*）グループの一意のID。

   *ID は一度作成すると変更できません。*

* **[!UICONTROL 名前]**

   （*オプション*）グループの表示名。

   デフォルトの値は ID です。

* **[!UICONTROL 説明]**

   （*オプション*）グループの目的と権限の説明。

* **[!UICONTROL メンバーをグループに追加]**

   （*オプション*）グループの最初のメンバーとして含めるパブリッシュ側のメンバーを選択します。

* **[!UICONTROL 保存]**&#x200B;を選択

## 承認された管理者 {#authorized-administrators}

Communitiesのメンバーコンソールでメンバーを操作する場合、適切な権限を持つユーザーとしてログインする必要があります。また、[tunnel service](deploy-communities.md#tunnel-service-on-author)で使用されるレプリケーションエージェントを正しく構成する必要があります。

`admin`としてサインインしていない場合、サインインしたユーザーは`administrators`ユーザーグループのメンバーである必要があります。

作成者](deploy-communities.md#replication-agents-on-author)の[複製エージェントも参照してください。
