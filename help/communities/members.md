---
title: メンバーコンソールとグループ管理コンソール
seo-title: Members & Groups Management Consoles
description: メンバーコンソールとグループ管理コンソールにアクセスする方法
seo-description: How to access Members and Groups Management consoles
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 37%

---

# メンバーコンソールとグループ管理コンソール {#members-groups-management-consoles}

## 概要 {#overview}

AEM Communities の機能の多くは、サイト訪問者に対して、パブリッシュ環境でコミュニティに参加する前に登録とサインインを求めます。ユーザー登録が必要なのはパブリッシュ環境に限られ、一般に *メンバー* 区別する *ユーザー* がオーサー環境に登録されている。

### パブリッシュ環境のメンバー（ユーザー） {#members-users-on-publish}

コミュニティメンバーコンソールとグループコンソールを使用して、 *公開* 環境は、 *作成者* 環境。 これは、 [トンネルサービス](deploy-communities.md#tunnel-service-on-author) が有効になっている。

### オーサー環境のユーザー {#users-on-author}

に登録されているユーザーとグループを管理するための *作成者* 環境のセキュリティコンソールを使用するには、が必要です。

* グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**.
* グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL グループ]**.

>[!NOTE]
>
>サンプルコンテンツがデプロイされて有効になっていると、オーサー環境とパブリッシュ環境の両方に多数のサンプルユーザーが存在します。を使用してを実行する場合、これらのユーザーは表示されません [nosamplecontent 実行モード](../../help/sites-administering/production-ready.md).

## メンバーコンソール {#members-console}

パブリッシュ環境で登録されたメンバーをオーサー環境で管理するには、次の場所にあるメンバーコンソールを使用します。

* グローバルナビゲーションから、 **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL メンバー]**

>[!CAUTION]
>
>メンバーコンソールを使用できない場合、 [トンネルサービス](deploy-communities.md#tunnel-service-on-author) が有効になっていません。

![member-console1](assets/member-console1.png)

### 検索 {#search-features}

の左側にあるサイドパネルアイコンを選択します。 `Members` ヘッダーを使用して、検索サイドパネルを開くかどうかを切り替えます。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

「 `Members` ヘッダーを使用して、検索サイドパネルを閉じます。

### メンバーの統計 {#member-statistics}

表示されている列 `Views`, `Posts`, `Follows` および `Likes` ユーザーがAdobe Analyticsを使用して 1 つ以上のコミュニティサイトのメンバーになっている場合に更新されます [有効](sites-console.md#analytics).

### CSV の書き出し {#export-csv}

の選択 `Export CSV` リンクを使用すると、すべてのメンバーがコンマ区切り値のリストとしてダウンロードされ、スプレッドシートに読み込むのに適しています。

列ヘッダーは次のとおりです。

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 新しいメンバーを作成 {#create-new-member}

選択 `Create Member` パブリッシュ環境でユーザーを作成する場合。

![create-member1](assets/create-member1.png)

### 一般 - メンバー詳細 {#general-member-details}

大部分のフィールドはオプションです。メンバーは後からフィールドに自分のプロファイルを入力できます。

* **[!UICONTROL ID]**

(*必須*) 許可可能 ID は、メンバーのログイン ID です。
デフォルトでは、ID は必須の電子メールアドレスの値に設定されています。*作成後は、ID を変更できません*.

* **[!UICONTROL メールアドレス]**

(*必須*) メンバーの電子メールアドレス。
メンバーは、プロファイルの更新時に電子メールアドレスを変更できます。i ID が電子メールアドレスにデフォルト設定されている場合、ID は *not* 電子メールアドレスが変更されたときに変更します。

* **[!UICONTROL パスワード]**

   (*必須*) ログインパスワード。

* **[!UICONTROL パスワードの確認入力]**

   (*必須*) 確認用のパスワードを再入力します。

* **[!UICONTROL メンバーをサイトに追加]**

   (*オプション*) メンバーをコミュニティサイトのメンバーグループに追加するには、既存のコミュニティサイトから選択します。

* **[!UICONTROL メンバーをグループに追加]**

   (*オプション*) 既存のメンバーグループから選択して、そのグループにメンバーを追加します。

* 選択 **[!UICONTROL 保存]**

### 一般 - アカウント設定 {#general-account-settings}

アカウント設定では、コミュニティ管理者は以下の設定をおこなうことができます。：

* **[!UICONTROL ステータス]**

   * 禁止メンバーがサインインできず、メンバーがページを表示したり、サインインが必要なアクティビティに参加したりできません。 彼らは未だにオープンなコミュニティサイトを匿名で訪問する可能性があります。

   * 禁止されていないメンバーはコミュニティサイトのすべての機能にアクセスできます。

   デフォルトは `Not Banned` です。

* **[!UICONTROL 貢献度の制限]**

   オンにすると、メンバーによるコンテンツの投稿機能は制限されます。
初期設定は、貢献度の制限の設定によって異なります。[メンバーの貢献度の制限](limits.md)を参照してください。

* **[!UICONTROL パスワードを変更]**

   既存のメンバーを変更する際に存在するリンク。 コミュニティ管理者がメンバーのパスワードをリセットする機能を提供します。

### 一般 - 写真 {#general-photo}

メンバーのアバターを設定するには、まず「**[!UICONTROL 画像をアップロード]**」を選択して、.jpg、.png、.tif、.gif のいずれかから画像の種類を選択します。画像の推奨サイズは、72 dpi での 240 x 240 ピクセルです。

### 一般 - メンバーをサイトに追加 {#general-add-member-to-sites}

1 つ以上のコミュニティサイトのメンバーグループにメンバーを追加できます。まず、テキストボックスにテキストを入力します。

### 一般 - メンバーをグループに追加 {#general-add-member-to-groups}

1 つ以上のメンバーグループにメンバーを追加できます。まず、テキストボックスにテキストを入力します。

### 「バッジ」タブ {#badges-tab}

この `BADGES` panel では、バッジを手動で割り当てたり、取り消したりすることができます。 バッジは通常、獲得するものですが、役割の割り当てに使用することもできます。

[スコアとバッジ](implementing-scoring.md)も参照してください。

![create-member2](assets/create-member2.png)

* **[!UICONTROL バッジを追加]**
   * 次の中から選択するための入力を開始 [使用可能なバッジ](badges.md). バッジを選択したら、各サイトまたはすべてのサイトを選択します。このサイトで、メンバーのアバターと共にバッジが表示されます。
   * 複数のバッジとサイトを選択できます。
* **[!UICONTROL バッジを削除]**
   * バッジの横にあるごみ箱アイコンを選択して、削除します。

## グループコンソール {#groups-console}

グループコンソールはオーサー環境から使用でき、パブリッシュ環境で登録されたメンバーグループの作成や管理をおこなうことができます。特に、以下の目的で使用されます。
* [権限を持つメンバーグループ](users.md#privilegedmembersgroups)
* のグループベースの割り当て [イネーブルメントリソース](resources.md)

グループコンソールにアクセスするには：
* グローバルナビゲーションから、 **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL グループ]**.

>[!CAUTION]
>
>[トンネルサービス](deploy-communities.md#tunnel-service-on-author)が有効でない場合、グループコンソールを使用することはできません。

### 新しいグループを作成 {#create-new-group}

選択 `Add Group` パブリッシュ環境でグループを作成する場合。

![group-console1](assets/group-console1.png)

パブリッシュ側の新しいメンバーグループを作成するには、以下のフィールドを指定します。

* **[!UICONTROL ID]**

   (*必須*) グループの一意の ID。

   *ID は一度作成すると変更できません。*

* **[!UICONTROL 名前]**

   (*オプション*) グループの表示名。

   デフォルトの値は ID です。

* **[!UICONTROL 説明]**

   (*オプション*) グループの目的と権限の説明。

* **[!UICONTROL メンバーをグループに追加]**

   (*オプション*) グループの最初のメンバーとして含めるパブリッシュ側のメンバーを選択します。

* 選択 **[!UICONTROL 保存]**

## 承認された管理者 {#authorized-administrators}

コミュニティメンバーコンソールでメンバーを操作する場合は、適切な権限を持つユーザーとして、および [トンネルサービス](deploy-communities.md#tunnel-service-on-author) が正しく設定されている必要があります。

次の名前でサインインしていない場合 `admin`の場合、サインインしたユーザーは `administrators` ユーザーグループ。

関連トピック [オーサー環境のレプリケーションエージェント](deploy-communities.md#replication-agents-on-author).
