---
title: SAML 2.0 認証ハンドラー
seo-title: SAML 2.0 Authentication Handler
description: AEM での SAML 2.0 認証ハンドラーについて説明します。
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6bc60122d2512a6f58c0204cd240a1b99a37ed93
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 58%

---

# SAML 2.0 認証ハンドラー{#saml-authentication-handler}

AEM には、[SAML](http://saml.xml.org/saml-specifications) 認証ハンドラーが付属しています。このハンドラーによって、[ バインディングを使用した ](http://saml.xml.org/saml-specifications)SAML`HTTP POST` 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。

サポート対象は次のとおりです。

* メッセージの署名と暗号化
* ユーザーの自動作成
* AEMの既存のグループとの同期
* サービスプロバイダーおよび ID プロバイダーが開始した認証

このハンドラーは、暗号化された SAML 応答メッセージをユーザーノード（`usernode/samlResponse`）に格納して、サードパーティのサービスプロバイダーとの通信を容易にします。

>[!NOTE]
>
>[AEM と SAML の統合のデモンストレーション](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)を参照してください。
>
>エンドツーエンドのコミュニティの記事については、[Integrating SAML with Adobe Experience Manager](https://helpx.adobe.com/jp/experience-manager/using/aem63_saml.html)を参照してください。

## SAML 2.0 認証ハンドラーの設定 {#configuring-the-saml-authentication-handler}

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
>SAML アサーションは署名されます。オプションとして暗号化することもできます。これを機能させるには、TrustStore の ID プロバイダーの公開証明書を少なくとも提供する必要があります。 詳しくは、[TrustStore への IdP 証明書の追加](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore)の節を参照してください。

**** Sling がこの認証ハンドラーを使用する PathRepository のパス。このプロパティが空の場合は、認証ハンドラーが無効になります。

**Service RankingOSGi Framework Service Ranking 値** は、このサービスを呼び出す順序を示します。これは整数値で、値が大きいほど優先順位が高くなります。

**IDP 証明書** エイリアスグローバルトラストストア内の IdP の証明書のエイリアス。このプロパティが空の場合は、認証ハンドラーが無効になります。設定方法は、以下の「AEM TrustStore への IdP 証明書の追加」を参照してください。

**SAML 認証** 要求の送信先の IDP の ID プロバイダー URL。このプロパティが空の場合は、認証ハンドラーが無効になります。

>[!CAUTION]
>
>ID プロバイダーのホスト名は **Apache Sling Referrer Filter** の OSGi 設定に追加する必要があります。詳しくは、[Web コンソール](/help/sites-deploying/configuring-osgi.md)に関する節を参照してください。

**このサービスプロバ** イダーを ID プロバイダーで一意に識別するサービスプロバイダーエンティティ IDID。このプロパティが空の場合は、認証ハンドラーが無効になります。

**デフォル** トのリダイレクト認証が成功した後にリダイレクトするデフォルトの場所。

>[!NOTE]
>
>この場所は、`request-path` Cookie が設定されていない場合にのみ使用されます。 設定されたパスの下に有効なログイントークンを使用せずにページをリクエストした場合、リクエストされたパスは cookie に保存されます
>認証が成功すると、ブラウザーはこの場所にリダイレクトされます。

**ユーザー ID 属** 性 CRX リポジトリでのユーザーの認証および作成に使用されるユーザー ID を含む属性の名前。

>[!NOTE]
>
>ユーザー ID は SAML アサーションの `saml:Subject` ノードではなく、この `saml:Attribute` から取得されます。

**Use** Encryption この認証ハンドラが暗号化された SAML アサーションを受け入れるかどうか。

**CRX ユーザーの自** 動作成：認証に成功した後、リポジトリ内の既存以外のユーザーを自動的に作成するかどうか。

>[!CAUTION]
>
>CRX ユーザーの自動作成が無効な場合は、ユーザーを手動で作成する必要があります。

**Add to Groups 認** 証が正常に完了した後、ユーザーを CRX グループに自動的に追加するかどうかを指定します。

**Group** Membership このユーザーを追加する必要がある CRX グループのリストを含む saml:Attribute の名前。

## AEM TrustStore への IdP 証明書の追加 {#add-the-idp-certificate-to-the-aem-truststore}

SAML アサーションは署名されます。オプションとして暗号化することもできます。そのためには、少なくともリポジトリ内の IDP の公開証明書を指定する必要があります。これをおこなうには、次の手順を実行する必要があります。

1. *http:/serveraddress:serverport/libs/granite/security/content/truststore.html* に移動します。
1. **[!UICONTROL Create TrustStore リンク]** を押します。
1. TrustStore のパスワードを入力して「**[!UICONTROL 保存]**」を押します。
1. 「**[!UICONTROL TrustStore を管理]**」をクリックします。
1. IdP 証明書をアップロードします。
1. 証明書エイリアスを記録します。以下の例では、エイリアスは **[!UICONTROL admin#1436172864930]** です。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM キーストアへのサービスプロバイダーキーと証明書チェーンの追加 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下の手順は必須です。それ以外の場合は、次の例外が発生します。`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 移動先：[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. `authentication-service` ユーザーを編集します。
1. 「**アカウント設定**」の「**キーストアを作成**」をクリックしてキーストアを作成します。

>[!NOTE]
>
>以下の手順は、ハンドラーがメッセージに署名または復号化できる必要がある場合にのみ必要です。

1. 「**秘密鍵ファイルを選択**」をクリックして秘密鍵ファイルをアップロードします。キーは PKCS#8 形式で、DER エンコードが必要です。
1. 「**証明書チェーンファイルを選択**」をクリックして証明書ファイルをアップロードします。
1. 以下のようにエイリアスを割り当てます。

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML 用のロガーの設定 {#configure-a-logger-for-saml}

SAML の設定ミスにより発生する可能性があるすべての問題をデバッグするようにロガーを設定することができます。手順は次のとおりです。

1. Web コンソール ( *http://localhost:4502/system/console/configMgr* ) に移動します。
1. **Apache Sling Logging Logger Configuration** というエントリを探してクリックします。
1. 次の設定でロガーを作成します。

   * **Log Level：** Debug
   * **Log File：** logs/saml.log
   * **Logger：** com.adobe.granite.auth.saml
