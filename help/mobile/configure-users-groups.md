---
title: ユーザーとユーザーグループの設定
description: このページでは、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするためのユーザーとグループの設定方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 3%

---

# ユーザーとユーザーグループの設定 {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

この章では、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするためのユーザーとグループの設定方法について説明します。

## AEM Mobile アプリケーションユーザーおよびグループ管理 {#aem-mobile-application-users-and-group-administration}

AEM アプリの権限モデルの整理と管理に役立つように、次の 2 つのグループを使用できます。

* アプリ管理者向けアプリ管理者
* アプリ作成者向け app-authors

### AEM Mobile アプリケーションコンテンツ作成者（app-author グループ） {#aem-mobile-application-content-authors-app-author-group}

app-author グループのメンバーは、ページ、テキスト、画像およびビデオを含むAEM モバイルアプリケーションのコンテンツをオーサリングする責任を負います。

#### グループ設定 – app-authors {#group-configuration-app-authors}

1. 「app-authors」という名前のユーザーグループを作成します。

   ユーザーAdmin Consoleに移動：[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   ユーザーグループ コンソール内から「+」ボタンを選択してグループを作成します。

   このグループの ID を「app-authors」に設定して、AEM内のモバイルアプリケーションのオーサリングに固有のオーサーユーザーグループであることを示します。

1. グループにメンバーを追加：作成者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   作成者グループに app-authors を追加

1. app-authors ユーザーグループを作成したので、「ユーザーAdmin Console[&#x200B; を使用して、個々のチームメンバーをこの新しいグループに追加でき &#x200B;](http://localhost:4502/libs/granite/security/content/useradmin.md) す。

   ![chlimage_1-19](assets/chlimage_1-19.png)

   ユーザーグループの編集

1. [&#x200B; 権限コンソール &#x200B;](http://localhost:4502/useradmin) に移動し、クラウドサービスを管理するための権限を追加します

   * /etc/cloudservices で（読み取り）

   >[!NOTE]
   >
   >アプリ作成者は、AEMからデフォルトの content-authors （作成者）グループを拡張して、/content/phonegap 下にコンテンツを作成する機能を継承します

### AEM Mobile アプリケーション管理者グループ（app-admins グループ） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins グループのメンバーは、app-authors **AND** に含まれているのと同じ権限でアプリケーションコンテンツを作成でき、さらに次の責任も負います。

* AEMでのPhoneGap BuildおよびAdobe Mobile Services クラウドサービスの設定
* アプリケーションのコンテンツ同期 OTA 更新のステージング、公開およびクリア

>[!NOTE]
>
>権限によって、AEM App Command Center で一部のユーザーアクションを使用できるかどうかが決まります。
>
>app-authors には、app-admins で使用できるオプションがいくつか用意されています。

#### グループ設定 – app-admins {#group-configuration-app-admins}

1. app-admins という名前のグループを作成します。
1. 次のグループを新しい app-admins グループに追加します。

   * content-authors
   * ワークフローユーザー

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. [&#x200B; 権限コンソール &#x200B;](http://localhost:4502/useradmin) に移動し、クラウドサービスを管理するための権限を追加します

   * /etc/cloudservices/mobileservices の（読み取り、変更、作成、削除、レプリケート）
   * /etc/cloudservices/phonegap-build の（読み取り、変更、作成、削除、レプリケート）

1. 同じ権限コンソールで、アプリコンテンツの更新をステージング、公開、クリアするための権限を追加します

   * （読み取り、変更、作成、削除、レプリケート）/etc/packages/mobileapp
   * /var/contentsync の（読み取り）

   >[!NOTE]
   >
   >パッケージレプリケーションは、アプリの更新をオーサーインスタンスからパブリッシュインスタンスに公開するために使用されます

   >[!CAUTION]
   >
   >/var/contentsync アクセスがデフォルトで拒否される。
   >
   >読み取り権限を省略すると、空の更新パッケージが作成およびレプリケートされる可能性があります。

1. 必要に応じて、このグループにメンバーを追加

## ダッシュボードタイルの権限 {#dashboard-tile-permissions}

ダッシュボードタイルでは、ユーザーが持つ権限に基づいて、様々なアクションが表示される場合があります。 以下に、各タイルで使用できるアクションを示します。

これらの権限に加えて、現在のアプリの設定に基づいて、アクションを表示/非表示にすることもできます。 例えば、PhoneGap クラウド設定がアプリに割り当てられていない場合、「リモートビルド」アクションを公開しても意味はありません。 これらは、以下の「**設定条件**」セクションに一覧表示されます。

### アプリを管理タイル {#manage-app-tile}

タイルには現在、権限が必要なアクションはありませんが、アプリケーションの詳細ページには次のアクションがあります。

* app-author および app-admin 用の *編集* （UIトリガー- jcr:write - /content/phonegap/{suffix}）
* *ダウンロード* app-author および app-admin 用（UIトリガー- /content/phonegap/{suffix}）

次の画像は、アプリのダウンロードと編集のオプションを示しています。

![chlimage_1-21](assets/chlimage_1-21.png)
