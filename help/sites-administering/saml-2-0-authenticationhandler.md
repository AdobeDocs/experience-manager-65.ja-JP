---
title: SAML 2.0 認証ハンドラー
seo-title: SAML 2.0 認証ハンドラー
description: AEM での SAML 2.0 認証ハンドラーについて説明します。
seo-description: AEM での SAML 2.0 認証ハンドラーについて説明します。
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 62%

---

# SAML 2.0 認証ハンドラー{#saml-authentication-handler}

AEM には、[SAML](http://saml.xml.org/saml-specifications) 認証ハンドラーが付属しています。このハンドラーによって、[ バインディングを使用した ](http://saml.xml.org/saml-specifications)SAML`HTTP POST` 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。

サポート対象は次のとおりです。

* メッセージの署名と暗号化
* ユーザーの自動作成
* AEM でグループを既存のグループに同期させる
* サービスプロバイダーおよびIDプロバイダーが開始した認証

このハンドラーは、暗号化された SAML 応答メッセージをユーザーノード（`usernode/samlResponse`）に格納して、サードパーティのサービスプロバイダーとの通信を容易にします。

>[!NOTE]
>
>[AEM と SAML の統合のデモンストレーション](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)を参照してください。
>
>エンドツーエンドのコミュニティの記事については、[Integrating SAML with Adobe Experience Manager](https://helpx.adobe.com/jp/experience-manager/using/aem63_saml.html)を参照してください。

## SAML 2.0 認証ハンドラーの設定  {#configuring-the-saml-authentication-handler}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)を使用すると、[SAML](http://saml.xml.org/saml-specifications) 2.0 認証ハンドラーの設定（**Adobe Granite SAML 2.0 Authentication Handler**）にアクセスできます。設定可能なプロパティを以下に示します。

>[!NOTE]
>
>SAML 2.0 認証ハンドラーはデフォルトでは無効になっています。このハンドラーを有効にするには、次のどちらかのプロパティを設定する必要があります。
>
>* ID プロバイダーの POST の URL
>* サービスプロバイダーのエンティティ ID

>



>[!NOTE]
>
>SAML アサーションは署名されます。オプションとして暗号化することもできます。そのためには、少なくとも TrustStore の ID プロバイダーの公開証明書を指定する必要があります。詳しくは、[TrustStore への IdP 証明書の追加](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore)の節を参照してください。

**** Slingがこの認証ハンドラーを使用するPathRepositoryのパス。このプロパティが空の場合は、認証ハンドラーが無効になります。

**Service** RankingOSGi Framework Service Ranking値。このサービスを呼び出す順序を示します。これは整数値で、値が大きいほど優先順位が高くなります。

**IDP証明書** エイリアスグローバルトラストストア内のIdPの証明書のエイリアス。このプロパティが空の場合は、認証ハンドラーが無効になります。設定方法は、以下の「AEM TrustStore への IdP 証明書の追加」を参照してください。

**SAML認証** 要求の送信先となるIDPのIDプロバイダーURL。このプロパティが空の場合は、認証ハンドラーが無効になります。

>[!CAUTION]
>
>ID プロバイダーのホスト名は **Apache Sling Referrer Filter** の OSGi 設定に追加する必要があります。詳しくは、[Web コンソール](/help/sites-deploying/configuring-osgi.md)に関する節を参照してください。

**このサービスプロバ** イダーをIDプロバイダーで一意に識別するサービスプロバイダーエンティティIDID。このプロパティが空の場合は、認証ハンドラーが無効になります。

**デフォル** トのリダイレクト：認証が成功した後にリダイレクトするデフォルトの場所。

>[!NOTE]
>
>この場所は、`request-path` Cookieが設定されていない場合にのみ使用されます。 設定されたパスの下に有効なログイントークンを指定せずにページを要求した場合、要求されたパスはcookieに保存されます
>認証が成功すると、ブラウザーはこの場所にリダイレクトされます。

**ユーザーID属** 性CRXリポジトリでのユーザーの認証および作成に使用されるユーザーIDを含む属性の名前。

>[!NOTE]
>
>ユーザー ID は SAML アサーションの `saml:Subject` ノードではなく、この `saml:Attribute` から取得されます。

**Use** Encryptionこの認証ハンドラーが暗号化されたSAMLアサーションを必要とするかどうか。

**CRXユーザーの自** 動作成：認証に成功した後、リポジトリ内の既存のユーザー以外を自動的に作成するかどうか。

>[!CAUTION]
>
>CRX ユーザーの自動作成が無効な場合は、ユーザーを手動で作成する必要があります。

**Add to Groups認証** が成功した後にユーザーをCRXグループに自動的に追加するかどうかを指定します。

**Group** Membershipこのユーザーを追加する必要があるCRXグループのリストを含むsaml:Attributeの名前。

## AEM TrustStore への IdP 証明書の追加 {#add-the-idp-certificate-to-the-aem-truststore}

SAML アサーションは署名されます。オプションとして暗号化することもできます。そのためには、少なくともリポジトリ内の IDP の公開証明書を指定する必要があります。これをおこなうには、次の手順を実行する必要があります。

1. *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*&#x200B;に移動します。
1. **[!UICONTROL Create TrustStoreリンク]**&#x200B;を押します。
1. TrustStore のパスワードを入力して「**[!UICONTROL 保存]**」を押します。
1. 「**[!UICONTROL TrustStore を管理]**」をクリックします。
1. IdP 証明書をアップロードします。
1. 証明書エイリアスを記録します。以下の例では、エイリアスは **[!UICONTROL admin#1436172864930]** です。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM キーストアへのサービスプロバイダーキーと証明書チェーンの追加 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下の手順は必須です。それ以外の場合は、次の例外がスローされます。`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 次の場所に移動します。[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. `authentication-service`ユーザーを編集します。
1. 「**アカウント設定**」の「**キーストアを作成**」をクリックしてキーストアを作成します。

>[!NOTE]
>
>以下の手順は、ハンドラーがメッセージに署名または復号化できる必要がある場合にのみ必要です。

1. 「**秘密鍵ファイルを選択**」をクリックして秘密鍵ファイルをアップロードします。キーはPKCS#8形式で、DERエンコードが必要です。
1. 「**証明書チェーンファイルを選択**」をクリックして証明書ファイルをアップロードします。
1. 以下のようにエイリアスを割り当てます。

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML 用のロガーの設定 {#configure-a-logger-for-saml}

SAML の設定ミスにより発生する可能性があるすべての問題をデバッグするようにロガーを設定することができます。手順は次のとおりです。

1. Webコンソール(*http://localhost:4502/system/console/configMgr*)に移動します。
1. **Apache Sling Logging Logger Configuration**&#x200B;というエントリを探してクリックします。
1. 次の設定でロガーを作成します。

   * **Log Level：** Debug
   * **Log File：** logs/saml.log
   * **Logger：** com.adobe.granite.auth.saml
