---
title: SAML サービスプロバイダーの設定
seo-title: SAML サービスプロバイダーの設定
description: ユーザーが指定したサードパーティの ID プロバイダー（IDP）経由で AEM Forms にログインして認証できるように、SAML を認証プロバイダーとして設定できます。
seo-description: ユーザーが指定したサードパーティの ID プロバイダー（IDP）経由で AEM Forms にログインして認証できるように、SAML を認証プロバイダーとして設定できます。
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 98%

---


# SAML サービスプロバイダーの設定{#configure-saml-service-provider-settings}

Security Assertion Markup Language（SAML）は、エンタープライズドメインまたはハイブリッドドメインの認証を設定するときに選択できるオプションの 1 つです。SAML は主に複数ドメインにわたる SSO をサポートするときに使用されます。SAML を認証プロバイダーとして設定すると、ユーザーは、指定したサードパーティの ID プロバイダー（IDP）経由で AEM Forms にログインし、認証されます。

SAML について詳しくは、[ Security Assertion Markup Language （SAML） V2.0 Technical Overview](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf) を参照してください。

1. 管理コンソールで、設定／User Management／設定／SAML サービスプロバイダーの設定をクリックします。
1. 「サービスプロバイダーのエンティティ ID」ボックスに、AEM Forms サービスプロバイダー実装の識別子として使用する固有 ID を入力します。また、この固有 ID は、IDP（例えば、`um.lc.com`）を設定するときにも指定します。AEM Forms にアクセスする URL も使用できます（例えば、`https://AEMformsserver`）。
1. 「サービスプロバイダーの Base URL」ボックスに、forms サーバーのベース URL を入力します（例えば、`https://AEMformsserver:8080`）。
1. （オプション）AEM forms で署名付き認証要求を IDP に送信する機能を有効にするには、以下のタスクを実行します。

   * Trust Manager を使用して、「Trust Store の種類」に「ドキュメント署名証明書」を選択した PKCS #12 形式の証明書を読み込みます。（[ローカル秘密鍵証明書の管理](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)を参照）。
   * 「サービスプロバイダーの証明書キーのエイリアス」リストから、Trust Store の証明書に割り当てたエイリアスを選択します。
   * 「書き出し」をクリックして URL コンテンツをファイルに保存し、そのファイルを IDP に読み込みます。

1. （オプション）「サービスプロバイダーの名前 ID ポリシー」リストから、SAML アサーションでユーザーを識別するときに IDP で使用する名前の形式を選択します。選択肢は、「未指定」、「電子メール」、および「Windows ドメイン修飾名」です。

   >[!NOTE]
   >
   >名前の形式では、大文字と小文字が区別されません。

1. （オプション）「ローカルユーザーに対して認証プロンプトを有効にする」を選択します。このオプションを選択すると、次の 2 つのリンクが表示されます。

   * サードパーティの SAML ID プロバイダーのログインページへのリンク。このページでは、エンタープライズドメインに属しているユーザーが認証できます。
   * AEM Forms のログインページへのリンク。このページでは、ローカルドメインに属しているユーザーが認証できます。

   このオプションが選択されていない場合、サードパーティの SAML ID プロバイダーのログインページに直接リンクされ、エンタープライズドメインに属しているユーザーが認証できます。

1. （オプション）「アーティファクトバインディングを有効にする」を選択して、アーティファクトバインディングのサポートを有効にします。デフォルトでは、SAML と共に POST バインディングが使用されます。ただし、アーティファクトバインディングを設定した場合は、このオプションを選択します。このオプションを選択すると、実際のユーザーアサーションはブラウザーの要求を通じては渡されません。代わりに、アサーションへのポインターが渡され、バックエンド Web サービス呼び出しを使用してアサーションが取得されます。
1. （オプション）「リダイレクトバインディングを有効にする」を選択して、リダイレクトを使用する SAML バインディングをサポートします。
1. （オプション）「カスタムプロパティ」で、追加のプロパティを指定します。追加のプロパティは name=value のペアで指定し、各ペアは新しい行によって区切られます。

   * SAML アサーション発行の有効期限がサードパーティのアサーションの有効期間に一致するよう、AEM Forms を設定できます。サードパーティ SAML アサーションのタイムアウトに従う場合は、「カスタムプロパティ」で次の行を追加します。

      `saml.sp.honour.idp.assertion.expiry=true`

   * RelayState を使用するための次のカスタムプロパティを追加して、ユーザーが正常に認証された後にリダイレクトされる URL を判断します。

      `saml.sp.use.relaystate=true`

   * 次のカスタムプロパティを追加して、カスタム Java Server Pages (JSP) のURLを設定します。これは ID プロバイダーの登録リストをレンダリングするのに使用されます。カスタム Web アプリケーションを展開しなかった場合は、デフォルトの User Management ページを使用してリストをレンダリングします。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 「保存」をクリックします。

