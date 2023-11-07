---
title: SAML サービスプロバイダーの設定
seo-title: Configure SAML service provider settings
description: SAML サービスプロバイダーの設定を指定し、指定したサードパーティの ID プロバイダー (IDP) を介してAEM forms にログインし、認証できるようにします。
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 10%

---

# SAML サービスプロバイダーの設定{#configure-saml-service-provider-settings}

セキュリティアサーションマークアップ言語 (SAML) は、エンタープライズドメインまたはハイブリッドドメインの認証を設定する際に選択できるオプションの 1 つです。 SAML は、主に複数のドメインで SSO をサポートするために使用されます。 SAML を認証プロバイダーとして設定した場合、ユーザーは、指定したサードパーティの ID プロバイダー (IDP) を介してAEM forms にログインし、認証します。

SAML について詳しくは、 [Security Assertion Markup Language (SAML) V2.0 の技術概要](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. 管理コンソールで、設定/User Management/設定/SAML サービスプロバイダーの設定をクリックします。
1. 「 Service Provider Entity ID 」ボックスに、AEM forms サービスプロバイダー実装の識別子として使用する一意の ID を入力します。 また、この一意の ID は、IDP（例えば `um.lc.com`）を設定するときにも指定します。AEM Forms にアクセスする URL も使用できます（例えば `https://AEMformsserver`）。
1. 「サービスプロバイダーの Base URL」ボックスに、Forms サーバーのベース URL を入力します（例えば `https://AEMformsserver:8080`）。
1. （オプション）署名済みの認証要求をAEM forms から IDP に送信できるようにするには、次のタスクを実行します。

   * Trust Manager を使用して、Trust Store の種類として「Document Signing Credential」を選択した状態で、PKCS #12形式の秘密鍵証明書を読み込みます。 ( 詳しくは、 [ローカル秘密鍵証明書の管理](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 「サービスプロバイダー秘密鍵証明書キーのエイリアス」リストで、Trust Store の秘密鍵証明書に割り当てたエイリアスを選択します。
   * 「書き出し」をクリックして URL コンテンツをファイルに保存し、そのファイルを IDP に読み込みます。

1. （オプション）「 Service Provider Name ID Policy 」リストで、SAML アサーションでユーザーを識別するために IDP で使用される名前の形式を選択します。 「未指定」、「電子メール」、「Windows ドメイン修飾名」のオプションがあります。

   >[!NOTE]
   >
   >名前の形式では大文字と小文字が区別されません。

1. （オプション）「Enable Authentication Prompt For Local Users」を選択します。 このオプションを選択すると、次の 2 つのリンクが表示されます。

   * サードパーティの SAML id プロバイダーのログインページへのリンク。エンタープライズドメインに属するユーザーが認証できます。
   * ローカルドメインに属するユーザーが認証できるAEM forms ログインページへのリンク。

   このオプションを選択しない場合、ユーザーはサードパーティの SAML ID プロバイダーのログインページに直接移動し、エンタープライズドメインに属するユーザーが認証できます。

1. （オプション）「アーティファクトバインディングを有効にする」を選択して、アーティファクトバインディングのサポートを有効にします。 デフォルトでは、POSTバインディングが SAML で使用されます。 ただし、アーティファクトバインディングを設定した場合は、このオプションを選択します。 このオプションを選択した場合、実際のユーザーアサーションはブラウザーリクエストを通じて渡されません。 代わりに、アサーションへのポインターが渡され、バックエンド Web サービス呼び出しを使用してアサーションが取得されます。
1. （オプション）「リダイレクトバインディングを有効にする」を選択して、リダイレクトを使用する SAML バインディングをサポートします。
1. （オプション）「Custom Properties」で、追加のプロパティを指定します。 追加のプロパティは、名前と値のペアを新しい行で区切って指定します。

   * サードパーティのアサーションの有効期間に一致する有効期間に対してAEM Forms が SAML アサーションを発行するように設定できます。 サードパーティ SAML アサーションのタイムアウトを遵守するには、カスタムプロパティに次の行を追加します。

     `saml.sp.honour.idp.assertion.expiry=true`

   * RelayState を使用するための次のカスタムプロパティを追加して、認証成功後にユーザーがリダイレクトされる URL を決定します。

     `saml.sp.use.relaystate=true`

   * 次のカスタムプロパティを追加して、カスタム Java Server Pages(JSP) の URL を設定します。この URL は、ID プロバイダーの登録済みリストをレンダリングするために使用されます。 カスタム Web アプリケーションをデプロイしていない場合は、デフォルトの User Management ページを使用してリストがレンダリングされます。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 保存をクリックします。
