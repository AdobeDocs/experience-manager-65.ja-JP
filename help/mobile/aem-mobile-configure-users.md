---
title: ユーザーとユーザーグループの設定
description: このページでは、ユーザーの役割と、モバイル On-Demand Services アプリのオーサリングと管理をサポートするためのユーザーとグループの設定方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 7%

---

# ユーザーとユーザーグループの設定 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

この章では、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするためのユーザーとグループの設定方法について説明します。

## AEM Mobile アプリケーションユーザーおよびグループ管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile アプリケーションコンテンツ作成者（app-author グループ） {#aem-mobile-application-content-authors-app-author-group}

app-author グループのメンバーは、ページ、テキスト、画像およびビデオを含むAEM モバイルアプリケーションのコンテンツをオーサリングする責任を負います。

#### グループ設定 – app-authors {#group-configuration-app-authors}

1. 「app-authors」という名前のユーザーグループを作成します。

   ユーザーAdmin Consoleに移動：[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   ユーザーグループ コンソール内から「+」ボタンを選択してグループを作成します。

   このグループの ID を「app-authors」に設定して、AEM内のモバイルアプリケーションのオーサリングに固有のオーサーユーザーグループであることを示します。

1. グループにメンバーを追加：作成者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. app-authors ユーザーグループを作成したので、「ユーザーAdmin Console[ を使用して、個々のチームメンバーをこの新しいグループに追加でき ](http://localhost:4502/libs/granite/security/content/useradmin.md) す。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 以下をAEM コンテンツ作成者グループに追加できます。

   （読み取り）:

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile アプリケーション管理者グループ（app-admins グループ） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins グループのメンバーは、app-authors **AND** に含まれているのと同じ権限でアプリケーションコンテンツを作成でき、さらに次の責任も負います。

* アプリケーションのステージング、公開、消去、コンテンツ同期 OTA の更新

>[!NOTE]
>
>権限によって、AEM App Command Center で一部のユーザーアクションを使用できるかどうかが決まります。
>
>app-authors には、app-admins で使用できるオプションがいくつか用意されています。

### グループ設定 – app-admins {#group-configuration-app-admins}

1. app-admins という名前のグループを作成します。
1. 次のグループを新しい app-admins グループに追加します。

   * content-authors
   * ワークフローユーザー

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >ワークフローユーザーは、PhoneGap Buildサービスを使用したリモートビルドに必要です

1. [ 権限コンソール ](http://localhost:4502/useradmin) に移動し、クラウドサービスを管理するための権限を追加します

   * /etc/cloudservices/mobileservices の（読み取り、変更、作成、削除、レプリケート）

1. 同じ権限コンソールで、アプリのコンテンツの更新をステージング、公開、クリアする権限を追加します。

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
1. コンテンツのエクスポートまたはアップロード

   * エクスポートテンプレートにアクセスするには、/etc/contentsync で（読み取り）
   * /var の（読み取り）読み取り時のパストラバーサル
   * /var/contentsync の（読み取り、書き込み、変更、削除）により、ContentSync にキャッシュされた書き出しコンテンツの書き込み、読み取り、クリーンアップを行います。

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services アプリケーションを作成するための他の 2 つの役割と責務について詳しくは、次の資料を参照してください。

* [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services アプリケーション用AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)
