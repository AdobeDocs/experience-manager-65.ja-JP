---
title: ユーザーおよびユーザーグループの設定
description: このページでは、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするようにユーザーとグループを設定する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# ユーザーとユーザーグループの設定 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

この章では、ユーザーの役割と、モバイルアプリのオーサリングと管理をサポートするようにユーザーとグループを設定する方法について説明します。

## AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

AEM Apps の権限モデルを整理および管理するのに役立つように、次の 2 つのグループを使用できます。

* アプリ管理者向け app-admins
* アプリ作成者向けの app-authors

### AEM Mobile Application Content Authors（app-author グループ） {#aem-mobile-application-content-authors-app-author-group}

app-authors グループのメンバーは、ページ、テキスト、画像、ビデオなど、AEMモバイルアプリケーションコンテンツのオーサリングを担当します。

#### グループ設定 — app-authors {#group-configuration-app-authors}

1. 「app-authors」という名前のユーザーグループを作成します。

   ユーザーAdmin Consoleに移動します。 [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   ユーザーグループコンソール内で「+」ボタンを選択し、グループを作成します。

   このグループの ID を「app-authors」に設定し、AEM内でのモバイルアプリケーションのオーサリングに特有の特定のタイプのオーサーユーザーグループであることを示します。

1. メンバーをグループに追加：作成者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   app-authors を Authors グループに追加します。

1. app-authors ユーザーグループを作成したら、 [ユーザーAdmin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   ユーザーグループの編集

1. 次に移動： [権限コンソール](http://localhost:4502/useradmin) クラウドサービスを管理する権限を追加します。

   * /etc/cloudservices に対する（読み取り）

   >[!NOTE]
   >
   >アプリ作成者は、AEMからデフォルトの content-authors(Authors) グループを拡張し、/content/phonegap の下にコンテンツを作成する機能を継承します。

### AEM Mobile Application Administrators グループ（app-admins グループ） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins グループのメンバーは、app-authors に含まれているのと同じ権限でアプリケーションコンテンツを作成できます **および** さらに、次のことも担当します。

* AEMでのPhoneGap BuildおよびAdobeMobile Services クラウドサービスの設定
* アプリケーションコンテンツ同期 OTA 更新のステージング、公開、クリア

>[!NOTE]
>
>権限は、AEM App コマンドセンターでの一部のユーザーアクションの可用性を決定します。
>
>一部のオプションは、app-admins で利用できる app-authors では利用できません。

#### グループ設定 — app-admins {#group-configuration-app-admins}

1. app-admins というグループを作成します。
1. 以下のグループを新しい app-admins グループに追加します。

   * content-authors
   * ワークフローユーザー

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 次に移動： [権限コンソール](http://localhost:4502/useradmin) クラウドサービスを管理する権限を追加します。

   * /etc/cloudservices/mobileservices で（読み取り、変更、作成、削除、複製）
   * /etc/cloudservices/phonegap-build で（読み取り、変更、作成、削除、複製）

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

## ダッシュボードタイルの権限 {#dashboard-tile-permissions}

ダッシュボードタイルには、ユーザーが持っている権限に基づいて様々なアクションが表示される場合があります。 次に、各タイルで使用できるアクションを示します。

これらの権限に加えて、現在のアプリの設定に基づいて、アクションの表示/非表示を切り替えることもできます。 例えば、PhoneGap クラウド設定がアプリに割り当てられていない場合、「リモートビルド」アクションを公開するポイントはありません。 これらは、以下の「 」の下にリストされます。**設定条件**&#39;セクション。

### アプリを管理タイル {#manage-app-tile}

現在、タイルには権限を必要とするアクションはありませんが、アプリケーションの詳細ページには次のアクションがあります。

* *編集* app-author および app-admin の場合 (UIトリガー- jcr:write - /content/phonegap/上{suffix})
* *ダウンロード* app-author および app-admin (UIトリガー- /content/phonegap/上{suffix})

以下の画像に、アプリの「ダウンロード」および「編集」オプションを示します。

![chlimage_1-21](assets/chlimage_1-21.png)
