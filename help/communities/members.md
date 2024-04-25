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

AEM Communitiesの機能を使用するには、多くの場合、サイト訪問者を登録してログインしてからパブリッシュ環境のコミュニティに参加する必要があります。 ユーザー登録は、パブリッシュ環境にのみ存在する必要があり、一般的にと呼ばれます *メンバー* 区別する *ユーザー* オーサー環境に登録されている。

### パブリッシュのメンバー（ユーザー） {#members-users-on-publish}

コミュニティメンバーコンソールおよびグループコンソールの使用、に登録されているメンバーおよびメンバーグループ *publish* 環境は以下から作成および管理できます *作成者* 環境。 これは、 [トンネル サービス](deploy-communities.md#tunnel-service-on-author) が有効になっています。

### オーサー環境のユーザー {#users-on-author}

に登録されているユーザーとグループの管理 *作成者* 環境の場合は、プラットフォームのセキュリティコンソールを使用する必要があります。

* グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**.
* グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL グループ]**.

>[!NOTE]
>
>サンプルコンテンツがデプロイされ、有効になっている状態では、オーサー環境とパブリッシュ環境の両方で多くのサンプルユーザーが存在します。 これらのユーザーは、で実行しているときは表示されません [nosamplecontent 実行モード](../../help/sites-administering/production-ready.md).

## メンバーコンソール {#members-console}

オーサー環境でメンバーコンソールにアクセスして、パブリッシュ環境に登録されているメンバーを管理するには、次の手順を実行します。

* グローバルナビゲーションから、を選択します。 **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL メンバー]**

>[!CAUTION]
>
>次の場合、メンバーコンソールを使用することはできません [トンネル サービス](deploy-communities.md#tunnel-service-on-author) が有効になっていません。

![メンバーコンソール](assets/member-console1.png)

### 検索 {#search-features}

の左側にあるサイドパネルアイコンを選択します `Members` 切り替えるヘッダーで検索サイドパネルを開きます。

![サイドパネルアイコンを検索。](assets/leftpanel-icon.png)


![メンバーコンソールのフィルターオプション](assets/member-console2.png)

の左側にある「検索」アイコンを選択します `Members` 検索サイドパネルを閉じるを切り替えるためのヘッダー。

### メンバーの統計 {#member-statistics}

表示する列 `Views`, `Posts`, `Follows` および `Likes` ユーザーがAdobe Analyticsで 1 つ以上のコミュニティサイトのメンバーである場合に更新されます [enabled](sites-console.md#analytics).

### CSV を書き出し {#export-csv}

の選択 `Export CSV` リンクすると、すべてのメンバーが、スプレッドシートへのインポートに適したコンマ区切りの値のリストとしてダウンロードされます。

列ヘッダーは次のとおりです

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 新しいメンバーを作成 {#create-new-member}

を選択 `Create Member` パブリッシュ環境でユーザーを作成するには、次の手順を実行します。

![新しいメンバーを作成ウィンドウ](assets/create-member1.png)

### 一般 – メンバーの詳細 {#general-member-details}

ほとんどのフィールドは、メンバーが後でプロファイルに入力できるオプションのフィールドです。

* **[!UICONTROL ID]**

（*必須*）認証可能な ID は、メンバーのログイン ID です。
デフォルトでは、ID は必要なメールアドレスの値に設定されます。
*作成後は ID を変更できません*.

* **[!UICONTROL メールアドレス]**

（*必須*） メンバーのメールアドレス。
メンバーは、プロファイルを更新する際にメールアドレスを変更できます。I ID がメールアドレスにデフォルト設定されている場合、ID は次のようになります *ではない* メールアドレスが変更された場合に変更します。

* **[!UICONTROL パスワード]**

  （*必須*） ログインパスワード。

* **[!UICONTROL パスワードを再入力]**

  （*必須*）確認用のパスワードを再入力します。

* **[!UICONTROL Sites へのメンバーの追加]**

  （*オプション*）既存のコミュニティサイトから選択して、メンバーをコミュニティサイトのメンバーグループに追加します。

* **[!UICONTROL グループへのメンバーの追加]**

  （*オプション*）既存のメンバーグループから選択して、そのグループにメンバーを追加します。

* 「**[!UICONTROL 保存]**」を選択します

### 一般 – アカウント設定 {#general-account-settings}

アカウント設定では、コミュニティ管理者が次の操作を行うことができます。

* **[!UICONTROL ステータス]**
   * 禁止メンバーはログインできず、ページの表示やログインが必要なアクティビティへの参加を妨げられています。 オープンなコミュニティサイトを匿名で訪問する場合もあります。

   * 禁止されていませんメンバーはコミュニティサイトへのフルアクセス権を持っています。

  デフォルトは `Not Banned` です。

* **[!UICONTROL 貢献度の制限]**

  オンにすると、メンバーがコンテンツを投稿する機能が制限されます。
デフォルトは、貢献度制限の設定によって異なります。
参照： [メンバーの貢献度の制限](limits.md).

* **[!UICONTROL パスワードの変更]**

  既存のメンバーを変更する際に存在するリンク。 コミュニティ管理者がメンバーのパスワードをリセットする機能を提供します。

### 一般 – 写真 {#general-photo}

メンバーのアバターを指定するには、まず、次の項目を選択します **[!UICONTROL 画像をアップロード]** .jpg、.png、.tif、または.gif タイプの画像を選択します。 画像の推奨サイズは 240 x 240 ピクセル、72 dpi です。

### 一般 – サイトへのメンバーの追加 {#general-add-member-to-sites}

メンバーは、1 つ以上のコミュニティサイトのメンバーグループに追加できます。 まず、テキストボックスにテキストを入力します。

### 一般 – グループへのメンバーの追加 {#general-add-member-to-groups}

メンバーは、1 つ以上のメンバーグループに追加できます。 まず、テキストボックスにテキストを入力します。

### 「バッジ」タブ {#badges-tab}

この `BADGES` パネルでは、バッジを手動で割り当てたり、取り消したりできます。 バッジは、割り当てられた役割に対して使用でき、通常は獲得したバッジです。

関連トピック [スコアおよびバッジ](implementing-scoring.md).

![メンバーシップ設定を編集ウィンドウ](assets/create-member2.png)

* **[!UICONTROL バッジを追加]**
   * 入力を開始して次から選択 [使用可能なバッジ](badges.md). バッジを選択したら、各サイトまたはすべてのサイトを選択します。メンバーのアバターと一緒にバッジを表示する必要があります。
   * 複数のバッジやサイトを選択できます。
* **[!UICONTROL バッジを削除]**
   * バッジの横にあるごみ箱アイコンを選択すると、バッジを削除できます。

## グループコンソール {#groups-console}

オーサー環境から使用できるグループコンソールを使用すると、パブリッシュ環境に登録されているメンバーグループを作成および管理できます。 以下の場合に特に役立ちます。 [権限のあるメンバーグループ](users.md#privilegedmembersgroups).

グループコンソールにアクセスするには：
* グローバルナビゲーションから、を選択します。 **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL グループ]**.

>[!CAUTION]
>
>次の場合、グループ コンソールを使用できません。 [トンネル サービス](deploy-communities.md#tunnel-service-on-author) が有効になっていません。

### 新しいグループを作成 {#create-new-group}

を選択 `Add Group` （パブリッシュ環境でグループを作成するため）。

![新規グループを作成ウィンドウ](assets/group-console1.png)

パブリッシュ側メンバーグループを作成するための必須フィールドは以下のとおりです。

* **[!UICONTROL ID]**

  （*必須*） グループユニーク ID。

  *作成した ID は変更できません。*

* **[!UICONTROL 名前]**

  （*オプション*） グループの表示名。

  デフォルト値は ID です。

* **[!UICONTROL 説明]**

  （*オプション*） グループの目的と権限の説明。

* **[!UICONTROL グループにメンバーを追加]**

  （*オプション*） グループの初期メンバーとして含めるパブリッシュ側メンバーを選択します。

* 「**[!UICONTROL 保存]**」を選択します

## 承認済み管理者 {#authorized-administrators}

Communities メンバーコンソールでメンバーを操作する場合は、適切な権限を持つユーザーとして、およびが使用するレプリケーションエージェントにログインする必要があります [トンネル サービス](deploy-communities.md#tunnel-service-on-author) を正しく設定すること。

次のユーザーとしてログインしていない場合： `admin`を選択した場合、ログインしたユーザーはのメンバーである必要があります `administrators` ユーザーグループ。

関連トピック [オーサー環境のレプリケーションエージェント](deploy-communities.md#replication-agents-on-author).
