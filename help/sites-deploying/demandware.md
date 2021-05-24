---
title: Salesforce Commerce Cloud
seo-title: Salesforce Commerce Cloud／Demandware
description: Salesforce Commerce Cloud／Demandware を使用した e コマースのデプロイ方法について学習します。
seo-description: Salesforce Commerce Cloud／Demandware を使用した e コマースのデプロイ方法について学習します。
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 68%

---


# Salesforce Commerce Cloud{#salesforce-commerce-cloud}

必要なeコマースパッケージをデプロイすると、eコマースフレームワークの全機能と共に、SalesforceCommerce Cloud/Demandware実装（デモカタログを含む）に付属するeコマース機能のリファレンス実装が提供されます。

## Salesforce Commerce Cloud を使用した e コマースに必要なパッケージ {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}

e コマース機能をインストールするには、以下が必要です。

* AEM e コマースフレームワーク：

   * AEM の標準インストールの一部です。

* AEM Demandware Commerce コンテンツパッケージ

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>この統合は、OCAPI バージョン 17.6 以降を使用するために設定された Salesforce Commerce Cloud／Demandware インスタンスをサポートします。

### Salesforce Commerce Cloud を使用した e コマースのインストール {#installation-of-ecommerce-with-salesforce-commerce-cloud}

（デモカタログ Geometrixx Outdoors を使用して）Demandware コマース統合設定で AEM をインストールするには、次の基本的な手順に従います。

1. [AEM をインストール](/help/sites-deploying/deploy.md)します。
1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用して、コンテンツパッケージをインストールします。
1. AEM で必要な補助ページを[作成](/help/sites-authoring/page-authoring.md)します。

>[!NOTE]
>
>パッケージをダウンロードするには、[パッケージ共有](/help/sites-administering/package-manager.md#package-share)に移動します。

AEM と Demandware Sandbox の間のサーバー接続を設定する必要があります。ほとんどの設定は、デフォルトのパスやライブラリなどを使用して、提供されているSiteGenisデモコンテンツパッケージと連携するように事前に設定されています。 コネクタを他のサイトやライブラリで使用する場合は、この設定を更新する必要があります。

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)に移動します。
1. 「Demandware Client」をクリックします。****
1. 必要に応じて、インスタンスのエンドポイントの IP またはホスト名を入力します。****

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 「**保存**」をクリックします。
1. 「Demandware TransportHandler Plugin for WebDAV」をクリックします。****
1. 「**WebDAV user**」と「**WebDAV user password**」を設定します。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 「**保存**」をクリックします。

#### レプリケーション {#replication}

パッケージのインストール後にレプリケーションを有効にする必要があります。次の点を確認してください。[https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>レプリケーションエージェントはデフォルトで情報ログレベルに設定されています。詳しい情報が必要な場合は、ログレベルをデバッグに切り替えることができます。

#### OAuth {#oauth}

OAuth クライアントは Demandware Sandbox インスタンスを使用するように設定されています。テストが目的の場合は、変更する必要はありません。

ステージングおよび実稼動システムの場合、OAuth クライアントに適切なクライアント ID とパスワードを設定する必要があります。

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)に移動します。
1. **Demandware Access Token provider**&#x200B;をクリックします。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 必要に応じて値を修正し、「Save」をクリックします。****

### Salesforce Commerce Cloud サンドボックス  {#salesforce-commerce-cloud-sandbox}

Demandware Sandbox は、新しい Velocity テンプレートエンジンを実行するように設定する必要があります。

>[!NOTE]
>
>次のウィザードは AEM Demandware コネクタに含まれるものではありません。これは、デモコンテンツパッケージの一部としてそのまま提供されており、SiteGenesis デモページをすばやく設定するのに役立ちます。

1. [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html)に移動します。
1. 「**編集**」をクリックします。
1. 値を確認し、「OK」をクリックします。****
1. 「初期化」をクリックします。****
1. WebDAVフォルダーに移動し、`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`などで、公開済みのテンプレートファイルを確認します。

   >[!NOTE]
   >
   >拡張子は`.vs`です。

1. また、書き出されたJSファイルとCSSファイル（例えば`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`の下）も確認します。

