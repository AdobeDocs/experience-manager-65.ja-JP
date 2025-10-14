---
title: メンバーコンソールとグループ管理コンソール
description: メンバーおよびグループ管理コンソールへのアクセス方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 3%

---


# メンバーコンソールとグループ管理コンソール {#members-groups-management-consoles}

## 概要 {#overview}

AEM Communitiesの機能を使用するには、多くの場合、サイト訪問者を登録してログインしてからパブリッシュ環境のコミュニティに参加する必要があります。 ユーザー登録は、パブリッシュ環境にのみ存在する必要があります。また、オーサー環境に登録されている *ユーザー* と区別するために、一般に *メンバー* と呼ばれます。

### Publishのメンバー（ユーザー） {#members-users-on-publish}

*パブリッシュ* 環境に登録されたメンバーやメンバーグループは、コミュニティメンバーコンソールやグループコンソールを使用して、*オーサー* 環境から作成および管理することができます。 これは、[&#x200B; トンネル サービス &#x200B;](deploy-communities.md#tunnel-service-on-author) が有効な場合にのみ可能です。

### オーサー環境のユーザー {#users-on-author}

*オーサー* 環境に登録されたユーザーとグループを管理するには、プラットフォームのセキュリティコンソールを使用する必要があります。

* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL ユーザー]** を選択します。
* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL グループ]** を選択します。

>[!NOTE]
>
>サンプルコンテンツがデプロイされ、有効になっている状態では、オーサー環境とパブリッシュ環境の両方で多くのサンプルユーザーが存在します。 これらのユーザーは、[nosamplecontent 実行モード &#x200B;](../../help/sites-administering/production-ready.md) で実行している場合は存在しません。

## メンバーコンソール {#members-console}

オーサー環境でメンバーコンソールにアクセスして、パブリッシュ環境に登録されているメンバーを管理するには、次の手順を実行します。

* グローバルナビゲーションから **[!UICONTROL ナビゲーション]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL メンバー]** を選択します

>[!CAUTION]
>
>[&#x200B; トンネル サービス &#x200B;](deploy-communities.md#tunnel-service-on-author) が有効になっていない場合、メンバーコンソールを使用することはできません。

![&#x200B; メンバーコンソール &#x200B;](assets/member-console1.png)

### 検索 {#search-features}

`Members` ヘッダーの左側にあるサイドパネルアイコンを選択して、検索サイドパネルを開く切り替えを行います。

![&#x200B; サイドパネルアイコンを検索。](assets/leftpanel-icon.png)


![&#x200B; メンバーコンソールのフィルターオプション &#x200B;](assets/member-console2.png)

`Members` ヘッダーの左側にある検索アイコンを選択して、検索側パネルの閉じる状態を切り替えます。

### メンバーの統計 {#member-statistics}

`Views`、`Posts`、`Follows`、`Likes` を表示する列は、ユーザーがAdobe Analytics [&#x200B; 有効 &#x200B;](sites-console.md#analytics) の 1 つ以上のコミュニティサイトのメンバーである場合に更新されます。

### CSV を書き出し {#export-csv}

`Export CSV` のリンクを選択すると、すべてのメンバーが、スプレッドシートへのインポートに適したコンマ区切りの値のリストとしてダウンロードされます。

列ヘッダーは次のとおりです

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 新しいメンバーを作成 {#create-new-member}

「`Create Member`」を選択して、パブリッシュ環境でユーザーを作成します。

![&#x200B; 新規メンバーの作成ウィンドウ &#x200B;](assets/create-member1.png)

### 一般 – メンバーの詳細 {#general-member-details}

ほとんどのフィールドは、メンバーが後でプロファイルに入力できるオプションのフィールドです。

* **[!UICONTROL ID]**

（*必須*）認証可能な ID は、メンバーのログイン ID です。
デフォルトでは、ID は必要なメールアドレスの値に設定されます。
*作成後は、ID を変更できません*。

* **[!UICONTROL メールアドレス]**

（*必須*）メンバーのメールアドレス。
メンバーは、プロフィールの更新時にメールアドレスを変更することができます。
ID がメールアドレスにデフォルト設定されている場合、メールアドレスが変更されても ID は変更 *されません*。

* **[!UICONTROL パスワード]**

  （*必須*） ログインパスワード。

* **[!UICONTROL パスワードを再入力]**

  （*必須*）確認のため、パスワードを再入力してください。

* **[!UICONTROL Sites へのメンバーの追加]**

  （*オプション*）既存のコミュニティサイトから選択して、メンバーをコミュニティサイトのメンバーグループに追加します。

* **[!UICONTROL グループへのメンバーの追加]**

  （*オプション*）既存のメンバーグループから選択して、そのグループにメンバーを追加します。

* 「**[!UICONTROL 保存]**」を選択します

### 一般 – アカウント設定 {#general-account-settings}

アカウント設定では、コミュニティ管理者が次の操作を行うことができます。

* **[!UICONTROL ステータス]**
   * 禁止
メンバーがログインできません。そのため、ページを表示したり、ログインが必要なアクティビティに参加することができません。 オープンなコミュニティサイトを匿名で訪問する場合もあります。

   * 禁止されていません
メンバーは、コミュニティサイトに対して完全なアクセス権を持ちます。

  デフォルトは `Not Banned` です。

* **[!UICONTROL 貢献度の制限]**

  オンにすると、メンバーがコンテンツを投稿する機能が制限されます。
デフォルトは、貢献度制限の設定によって異なります。
[&#x200B; メンバーの貢献度の制限 &#x200B;](limits.md) を参照してください。

* **[!UICONTROL パスワードの変更]**

  既存のメンバーを変更する際に存在するリンク。 コミュニティ管理者がメンバーのパスワードをリセットする機能を提供します。

### 一般 – 写真 {#general-photo}

メンバーのアバターを指定するには、まず **[!UICONTROL 画像をアップロード]** を選択し、.jpg、.png、.tif または.gif タイプの画像を選択します。 画像の推奨サイズは 240 x 240 ピクセル、72 dpi です。

### 一般 – サイトへのメンバーの追加 {#general-add-member-to-sites}

メンバーは、1 つ以上のコミュニティサイトのメンバーグループに追加できます。 まず、テキストボックスにテキストを入力します。

### 一般 – グループへのメンバーの追加 {#general-add-member-to-groups}

メンバーは、1 つ以上のメンバーグループに追加できます。 まず、テキストボックスにテキストを入力します。

### 「バッジ」タブ {#badges-tab}

`BADGES` パネルでは、バッジを手動で割り当てたり、取り消したりできます。 バッジは、割り当てられた役割に対して使用でき、通常は獲得したバッジです。

[&#x200B; スコアおよびバッジ &#x200B;](implementing-scoring.md) も参照してください。

![&#x200B; メンバーシップ設定を編集ウィンドウ &#x200B;](assets/create-member2.png)

* **[!UICONTROL バッジを追加]**
   * 入力を開始し、[&#x200B; 使用可能なバッジ &#x200B;](badges.md) から選択します。 バッジを選択したら、各サイトまたはすべてのサイトを選択します。メンバーのアバターと一緒にバッジを表示する必要があります。
   * 複数のバッジやサイトを選択できます。
* **[!UICONTROL バッジを削除]**
   * バッジの横にあるごみ箱アイコンを選択すると、バッジを削除できます。

## グループコンソール {#groups-console}

オーサー環境から使用できるグループコンソールを使用すると、パブリッシュ環境に登録されているメンバーグループを作成および管理できます。 これは、特に [&#x200B; 権限のあるメンバーグループ &#x200B;](users.md#privilegedmembersgroups) で役立ちます。

グループコンソールにアクセスするには：
* グローバルナビゲーションから **[!UICONTROL ナビゲーション]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL グループ]** を選択します。

>[!CAUTION]
>
>[&#x200B; トンネル サービス &#x200B;](deploy-communities.md#tunnel-service-on-author) が有効になっていない場合、グループ コンソールは使用できません。

### 新しいグループを作成 {#create-new-group}

「`Add Group`」を選択して、パブリッシュ環境でグループを作成します。

![&#x200B; 新規グループを作成ウィンドウ &#x200B;](assets/group-console1.png)

パブリッシュ側メンバーグループを作成するための必須フィールドは以下のとおりです。

* **[!UICONTROL ID]**

  （*必須*）グループの一意の ID。

  *作成後は、ID を変更できません。*

* **[!UICONTROL 名前]**

  （*オプション*）グループの表示名。

  デフォルト値は ID です。

* **[!UICONTROL 説明]**

  （*オプション*）グループの目的と権限の説明。

* **[!UICONTROL グループにメンバーを追加]**

  （*オプション*）グループの初期メンバーとして含めるパブリッシュ側メンバーを選択します。

* 「**[!UICONTROL 保存]**」を選択します

## 承認済み管理者 {#authorized-administrators}

Communities メンバーコンソールでメンバーを操作する場合は、適切な権限を持つユーザーとしてログインし、[&#x200B; トンネルサービス &#x200B;](deploy-communities.md#tunnel-service-on-author) で使用されるレプリケーションエージェントを正しく設定する必要があります。

`admin` としてログインしていない場合、ログインしたユーザーは `administrators` ユーザーグループのメンバーである必要があります。

[&#x200B; 作成者のレプリケーションエージェント &#x200B;](deploy-communities.md#replication-agents-on-author) も参照してください。
