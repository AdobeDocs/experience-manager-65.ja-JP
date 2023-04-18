---
title: ユーザーおよびユーザーグループの設定
description: このページでは、ユーザーの役割と、Mobile On-Demand Services アプリのオーサリングと管理をサポートするようにユーザーとグループを設定する方法について説明します。
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# ユーザーとユーザーグループの設定 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

この章では、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするようにユーザーとグループを設定する方法について説明します。

## AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

### AEM Mobile Application Content Authors（app-author グループ） {#aem-mobile-application-content-authors-app-author-group}

app-authors グループのメンバーは、ページ、テキスト、画像およびビデオなど、AEMモバイルアプリケーションコンテンツのオーサリングを担当します。

#### グループ設定 — app-authors {#group-configuration-app-authors}

1. 「app-authors」という新しいユーザーグループを作成します。

   ユーザーAdmin Consoleに移動します。 [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   ユーザーグループコンソール内で「+」ボタンを選択し、グループを作成します。

   このグループの ID を「app-authors」に設定し、AEM内でのモバイルアプリケーションのオーサリングに特有の特定のタイプのオーサーユーザーグループであることを示します。

1. メンバーをグループに追加：発言者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. app-authors ユーザーグループを作成したら、 [ユーザー管理コンソール](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 次のオプションを使用して、AEM Content Authors グループに追加できます。

   （読み取り）

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile Application Administrators グループ（app-admins グループ） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins グループのメンバーは、app-authors に含まれているのと同じ権限でアプリケーションコンテンツを作成できます **および** また、次のことも担当します。

* アプリケーションの ContentSync OTA 更新のステージング、公開、クリア

>[!NOTE]
>
>権限は、AEM App コマンドセンターでの一部のユーザーアクションの可用性を決定します。
>
>app-admins で利用できる app-authors では、一部のオプションが利用できません。

### グループ設定 — app-admins {#group-configuration-app-admins}

1. app-admins という新しいグループを作成します。
1. 以下のグループを新しい app-admins グループに追加します。

   * content-authors
   * ワークフローユーザー

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >workflow-users は、PhoneGap Buildサービスを使用したリモートビルドに必要です

1. 次に移動： [権限コンソール](http://localhost:4502/useradmin) クラウドサービスを管理する権限を追加します。

   * /etc/cloudservices/mobileservices で（読み取り、変更、作成、削除、複製）

1. 同じ権限コンソールで、アプリコンテンツの更新をステージング、公開、クリアする権限を追加します。

   * /etc/packages/mobileapp で（読み取り、変更、作成、削除、複製）
   * /var/contentsync に対する（読み取り）

   >[!NOTE]
   >
   >パッケージレプリケーションは、アプリの更新をオーサーインスタンスからパブリッシュインスタンスに公開するために使用されます

   >[!CAUTION]
   >
   >/var/contentsync アクセスが拒否されました。
   >
   >読み取り権限を省略すると、空の更新パッケージが作成およびレプリケートされる可能性があります。

1. 必要に応じてこのグループにメンバーを追加します
1. コンテンツを書き出しまたはアップロードするには

   * 書き出しテンプレートにアクセスするには、 /etc/contentsync で（読み取り）を実行します。
   * 読み取り時のパストラバーサル用に/var に対して（読み取り）
   * /var/contentsync の（読み取り、書き込み、変更、削除）。ContentSync でキャッシュされた書き出しコンテンツの書き込み、読み取り、クリーンアップを行います。

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services App の作成に関する他の 2 つの役割と責務について詳しくは、次のリソースを参照してください。

* [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesアプリ用AEMコンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)
