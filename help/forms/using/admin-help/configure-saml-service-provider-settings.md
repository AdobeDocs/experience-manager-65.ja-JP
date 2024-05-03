---
title: SAML サービスプロバイダーの設定
description: 指定したサードパーティの ID プロバイダー（IDP）経由で、ユーザーが AEM Forms にログインして認証できるように、SAML サービスプロバイダー設定を指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 100%

---

# SAML サービスプロバイダーの設定{#configure-saml-service-provider-settings}

Security Assertion Markup Language（SAML）は、エンタープライズドメインまたはハイブリッドドメインの認証を設定するときに選択できるオプションの 1 つです。SAML は主に複数ドメインにわたる SSO をサポートするときに使用されます。SAML を認証プロバイダーとして設定すると、ユーザーは、指定したサードパーティの ID プロバイダー（IDP）経由で、ユーザーは AEM Forms にログインし、認証されます。

SAML について詳しくは、[Security Assertion Markup Language（SAML）V2.0 Technical Overview](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) を参照してください。

1. 管理コンソールで、設定／User Management／設定／SAML サービスプロバイダーの設定をクリックします。
1. 「サービスプロバイダーのエンティティ ID」ボックスに、AEM Forms サービスプロバイダー実装の識別子として使用する一意の ID を入力します。また、この一意の ID は、IDP（例えば `um.lc.com`）を設定するときにも指定します。AEM Forms にアクセスする URL も使用できます（例えば `https://AEMformsserver`）。
1. 「サービスプロバイダーのベース URL」ボックスに、Forms サーバーのベース URL を入力します（例：`https://AEMformsserver:8080`）。
1. （オプション）署名済みの認証リクエストを AEM Forms から IDP に送信できるようにするには、次のタスクを実行します。

   * Trust Manager を使用して、「Trust Store の種類」として選択した「ドキュメント署名証明書」付きの PKCS #12 形式の証明書を読み込みます。（[ローカル資格情報の管理](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)を参照）。
   * 「サービスプロバイダーの資格情報キーのエイリアス」リストから、Trust Store の資格情報に割り当てたエイリアスを選択します。
   * 「書き出し」をクリックすると、URL コンテンツをファイルに保存し、そのファイルを IDP に読み込めます。

1. （オプション）「サービスプロバイダーの名前 ID ポリシー」リストから、SAML アサーションでユーザーを識別するときに IDP で使用する名前の形式を選択します。選択肢は、「未指定」、「メール」および「Windows ドメイン修飾名」です。

   >[!NOTE]
   >
   >名前の形式では、大文字と小文字が区別されません。

1. （オプション）「ローカルユーザーに対して認証プロンプトを有効にする」を選択します。このオプションを選択すると、次の 2 つのリンクが表示されます。

   * サードパーティの SAML ID プロバイダーのログインページへのリンク。このページでは、エンタープライズドメインに属しているユーザーが認証できます。
   * AEM Forms のログインページへのリンク。このページでは、ローカルドメインに属しているユーザーが認証できます。

   このオプションが選択されていない場合、サードパーティの SAML ID プロバイダーのログインページに直接リンクされ、エンタープライズドメインに属しているユーザーが認証できます。

1. （オプション）「アーティファクトバインディングを有効にする」を選択して、アーティファクトバインディングのサポートを有効にします。デフォルトでは、SAML と共に POST バインディングが使用されます。ただし、アーティファクトバインディングを設定した場合は、このオプションを選択します。このオプションを選択すると、実際のユーザーアサーションはブラウザーリクエストを通じては渡されません。代わりに、アサーションへのポインターが渡され、バックエンド web サービス呼び出しを使用してアサーションが取得されます。
1. （オプション）「リダイレクトバインディングを有効にする」を選択して、リダイレクトを使用する SAML バインディングをサポートします。
1. （オプション）「カスタムプロパティ」で、追加のプロパティを指定します。追加のプロパティは新しい行で区切られた名前=値のペアです。

   * SAML アサーション発行の有効期限がサードパーティのアサーションの有効期間に一致するよう、AEM Forms を設定できます。サードパーティ SAML アサーションのタイムアウトに従う場合は、「カスタムプロパティ」で次の行を追加します。

     `saml.sp.honour.idp.assertion.expiry=true`

   * RelayState を使用するための次のカスタムプロパティを追加して、ユーザーが正常に認証された後にリダイレクトされる URL を判断します。

     `saml.sp.use.relaystate=true`

   * 次のカスタムプロパティを追加して、カスタム Java™ Server Pages（JSP）の URL を設定します。これは ID プロバイダーの登録リストをレンダリングするのに使用されます。カスタム web アプリケーションをデプロイしなかった場合、デフォルトの User Management ページを使用してリストをレンダリングします。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 「保存」をクリックします。
