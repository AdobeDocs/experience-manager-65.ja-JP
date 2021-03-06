---
title: Adobe Analytics および Adobe Target との統合のオプトイン
seo-title: Opting Into Adobe Analytics and Adobe Target
description: Adobe Analytics および Adobe Target との統合をオプトインする方法について説明します。
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 100%

---

# Adobe Analytics および Adobe Target との統合のオプトイン{#opting-into-adobe-analytics-and-adobe-target}

AEM には、Adobe Analytics および Adobe Target との統合に役立つオプトイン手順が用意されています。このタスクは、あらかじめ読み込まれて管理者ユーザーグループに割り当てられており、すぐに使用できます。

管理者としてログインすると、このタスク（**Analytics &amp; Targeting を設定**）を[インボックス](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)から使用できます。指定された資格情報に基づいて、これらのサービスを設定および統合できます。

統合の設定には、次のオプションがあります。

* タスクによる統合の設定。

   この設定は、すぐに行うことも、後で行うこともできます。タスクは、何らかのアクションが実行されるまでインボックスに残ります。どちらの場合でも、UI で直接設定することも、事前定義済みの `.properties` ファイルを使用して設定することもできます。

* 統合のオプトアウト。

   [手動で統合を設定する](/help/sites-administering/marketing-cloud.md)場合は、このオプションを検討してください。[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=ja)も参照してください。

* スクリプトを使用してセットアップとプロビジョニングを設定します。

## 統合の設定 {#configuring-the-integration}

次との統合をオプトインします。

* Analytics（ページ追跡および分析機能を使用できます）
* Target（パーソナライゼーション機能を使用できます）

どちらのオプションでも、ユーザーアカウント情報を設定して、追跡するページを指定する必要があります。

>[!NOTE]
>
>オプションで、サーバーの起動時に読み込まれるプロパティファイルを使用して、Analytics および Target のアカウント情報を設定できます。[プロパティファイルを使用したアカウント情報の設定](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)を参照してください。

統合をオプトインすると、AEM が次のタスクを実行します。

* Analytics および Target への接続を可能にするクラウド設定を作成する。
* 追跡するデータを決定するフレームワークを作成する。
* これらのサービスを使用するために Web ページを設定する。

>[!NOTE]
>
>AT.js は、デフォルトのクライアントライブラリです。これは、[Target のクラウドサービス設定](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration)で設定されています。
>
>AT.js をクライアントライブラリとして使用することをお勧めします。

事前に読み込まれた標準タスクからオプトインするには：

1. [インボックスから、Analytics &amp; Targeting の設定](/help/sites-authoring/inbox.md#taking-action-on-an-item)タスクを選択して&#x200B;**開きます**。

   ![optin-01](assets/optin-01.png)

1. Analytics の場合：

   1. Analytics のユーザーアカウント情報を入力し、対応する「**追加**」ボタンをクリックします。
   1. 適切な資格情報が認証されます。
   1. Analytics アカウントが認証されたら、使用する Analytics レポートスイートを選択します。AEM がこれらの Analytics レポートスイートを取得します。ステータスが「**追加済み**」に更新されます。

1. Target の場合：

   1. Target のユーザーアカウント情報を入力し、対応する「**追加**」ボタンをクリックします。
   1. 適切な資格情報が認証されます。ステータスが「**追加済み**」に更新されます。

1. 「**次へ**」を選択します。
1. Analytics や Target を使用する必要のあるサイトを選択します。

1. 「**完了**」を選択して完了します。

   >[!CAUTION]
   >
   >設定をオプトインしたら、その変更内容をパブリッシュインスタンスにレプリケーションするために、影響を受けるサイト／ページを公開する必要があります。

## 統合のオプトアウト {#opting-out-of-the-integration}

次の場合に、Analytics および Target との統合をオプトアウトします。

* これらの製品と統合したくない。
* 手動で統合を設定したい。

   手動での統合の設定については、[Adobe Analytics との統合](/help/sites-administering/adobeanalytics.md)および [Adobe Target との統合](/help/sites-administering/target.md)を参照してください。

オプトアウトするには、事前に読み込まれたタスクを完了する必要があります。

* [インボックスから、Analytics &amp; Targeting を設定タスクを選択して&#x200B;**完了**&#x200B;します。](/help/sites-authoring/inbox.md#taking-action-on-an-item)

## プロパティファイルを使用したアカウント情報の設定 {#providing-account-information-using-a-properties-file}

Analytics および Target との統合用のアカウントプロパティを設定するために AEM がサーバーの起動時に読み込むプロパティファイルをインストールします。プロパティファイルを使用すると、オプトインウィザードにファイルのプロパティが自動的に設定され、それに従ってクラウド設定が作成されます。

プロパティファイルは marketingcloud.properties という名前のテキストファイルで、AEM プロセスが使用する作業ディレクトリ（通常は JAR ファイルと同じディレクトリ）に保存します。このファイルには次のプロパティが含まれます。

* analytics.server：使用する Analytics データセンターの URL。
* analytics.company：Analytics ユーザーアカウントに関連付けられた会社。
* analytics.username：Analytics ユーザー名。
* analytics.secret：Analytics ユーザー名に関連付けられた秘密鍵。
* analytics.reportsuite：使用する Analytics レポートスイートの名前。
* target.clientcode：Target アカウントに関連付けられたクライアントコード。
* target.email：Target アカウントの認証に使用する電子メールアドレス。
* target.password：電子メールアドレスに関連付けられたパスワード。

プロパティと値は等号（=）で区切ります。Analytics プロパティの先頭には `analytics` が付き、Target プロパティの先頭には `target` が付きます。サービスを設定するには、そのサービスのすべてのプロパティの値を設定します。サービスを設定しない場合は、そのサービスの値を設定しないでください。

次の `.properties` ファイルのサンプルには、Analytics 用のクラウド設定を作成するためのプロパティ値が含まれています。

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

プロパティファイルを使用して統合をオプトインする手順を以下に示します。

1. AEM プロセスが使用する作業ディレクトリ（オーサーインスタンス）に `marketingcloud.properties` ファイルを作成します。

   >[!NOTE]
   >
   >作業ディレクトリは、通常 jar または `license.properties` ファイルを保持するディレクトリです。
   >
   >ただし、システムプロパティによる絶対パスとして定義することもできます。
   >
   >`mac.provisioning.file.container`

1. Analytics または Target のアカウントに従って、プロパティ値を追加します。
1. サーバーを起動または再起動し、管理者アカウントを使用してログインします。
1. [統合の設定](/help/sites-administering/opt-in.md#configuring-the-integration)で説明されているように、Analytics &amp; Targeting を設定タスクを開きます。アカウント情報を要求する代わりに、ウィザードに `.properties` ファイルの値が設定されます。

   適切なサービスに対して&#x200B;**追加**&#x200B;を選択し、ウィザードを続行します。

   ![optin-02](assets/optin-02.png)

## クラウド設定について {#about-the-cloud-configurations}

Analytics および Target との統合を設定すると、必要なクラウド設定とフレームワークを AEM が自動的に作成します。例えば、Analytics のクラウド設定は Provisioned Analytics Account という名前です。

このクラウド設定を変更する必要はありません。ただし、必要に応じてフレームワークを設定できます（[コンポーネントデータと Adobe Analytics プロパティのマッピング](/help/sites-administering/adobeanalytics-mapping.md)および [Target フレームワークの追加](/help/sites-administering/target.md)を参照）

>[!NOTE]
>
>デフォルトでは、Adobe Target 設定ウィザードをオプトインすると、正確なターゲット設定が有効になります。
>
>正確なターゲット設定を有効にすると、クラウドサービス設定はコンテンツが読み込まれるまでコンテキストの読み込みを待機します。結果として、正確なターゲット設定を有効にすると、パフォーマンスの面ではコンテンツの読み込みに数ミリ秒の遅延が発生することがあります。
>
>正確なターゲット設定はオーサーインスタンスでは常に有効になっています。ただし、パブリッシュインスタンスではクラウドサービス設定（**http://localhost:4502/etc/cloudservices.html**）の正確なターゲット設定の横にあるチェックマークをオフにすることで、正確なターゲット設定をグローバルにオフにできます。また、クラウドサービス設定の設定に関係なく、個々のコンポーネントの正確なターゲット設定のオンとオフを切り替えることもできます。
>
>この設定を変更しても、作成済みの対象コンポーネントには影響しません&#x200B;***。***&#x200B;これらのコンポーネントには直接変更を加える必要があります。

>[!CAUTION]
>
>Analytics 設定をオプトインして特定の `reportsuite` が選択されると、フレームワークがパブリッシュ実行モードに制限されます。これは、パブリッシュインスタンスに対してのみトラッキングが機能することを意味します。
>
>トラッキングがオーサーインスタンスでも必要な場合は、値を `all` に変更する必要があります。

## スクリプトを使用したセットアップとプロビジョニングの設定 {#configuring-the-setup-and-provisioning-via-script}

管理者の場合、ウィザードの手順に従って手動でおこなう代わりに、スクリプトを使用してセットアップとプロビジョニングを実行できます。手順は次のとおりです。

* POST リクエストと必要なパラメーターを **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** に送信します。

送信するパラメーターは、次のように場合によって異なります。

* 必要な資格情報がすべて入力された **marketingcloud.properties** ファイルを使用する場合は、次のパラメーターを送信する必要があります。

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=作成したクラウドサービス設定を接続する AEM ページへのパス

   例えば、Analytics と Target の両方の設定を作成し、それらを we.retail ページに添付する cURL リクエストは次のとおりです。

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* **marketingcloud.properties** ファイルを使用しない場合は、パラメーターと共に資格情報を送信する必要があります。次に例を示します。

   * automaticProvisioning= `true`
   * serviceName= `analytics|target`
   * path=作成したクラウドサービス設定を接続する AEM ページへのパス（複数のパスを定義可能）
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   この場合、Analytics と Target の両方の設定を作成し、それらを we-retail ページに添付する cURL リクエストは次のようになります。

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
