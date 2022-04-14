---
title: シングルサインオン
seo-title: Single Sign On
description: AEM インスタンスに対するシングルサインオン（SSO）を設定する方法について学習します。
seo-description: Learn how to configure Single Sign On (SSO) for an AEM instance.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuring
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '740'
ht-degree: 100%

---

# シングルサインオン {#single-sign-on}

シングルサインオン（SSO）は、ユーザーが認証の資格情報（ユーザー名、パスワードなど）を一度入力すれば、その後は複数のシステムにアクセスできるようにするものです。個別のシステム（信頼された認証として知られる）が認証を実行し、Adobe Experience Manager に対してユーザーの資格情報を提供します。Adobe Experience Manager がそのユーザーのアクセス権を確認し、適用します（つまり、ユーザーがアクセスを許可されているリソースを決定します）。

SSO 認証ハンドラーサービス（`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`）は、信頼された認証が提供する認証結果を処理します。 SSO 認証ハンドラーは、次の順序で特別な属性の値として ssid（SSO 識別子）を検索します。

1. 要求ヘッダー
1. cookie
1. 要求パラメーター

値が見つかった場合は、検索を終了し、その値を使用します。

以下の 2 つのサービスについて、この ssid が格納された属性の名前を認識できるように設定します。

* ログインモジュール
* SSO 認証サービス

両方のサービスに同じ属性名を指定する必要があります。 属性は `Repository.login` に提供される `SimpleCredentials` が含められます。属性の値は無関係で無視されます。単に存在していることが重要で検証されます。

## SSO の設定 {#configuring-sso}

AEM インスタンス用に SSO を設定するには、[SSO Authentication Handler](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler) を設定する必要があります。

1. AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

   例えば、NTLM の場合は以下のように設定します。

   * **パス：**&#x200B;必要に応じて設定します（`/` など）。
   * **ヘッダー名**：`LOGON_USER`
   * **ID 形式**：`^<DOMAIN>\\(.+)$`

       `<*DOMAIN*>` を独自のドメイン名に置き換えてください。
   CoSign の場合：

   * **パス：**&#x200B;必要に応じて設定します（`/` など）。
   * **ヘッダー名**：remote_user
   * **ID 形式**：AsIs

   SiteMinder の場合：

   * **パス**：必要に応じて設定します（`/` など）。
   * **ヘッダー名**：SM_USER
   * **ID 形式**：AsIs



1. 認証を含め、シングルサインオンが要求どおりに動作していることを確認します。

>[!CAUTION]
>
>SSO を設定した場合は、ユーザーが直接 AEM にアクセスできないようにしてください。
>
>SSO システムのエージェントを実行する Web サーバー経由でアクセスするようにユーザーに要求します。そうすることで、ユーザーが AEM から信頼されるためのヘッダー、cookie またはパラメーターを直接送信できなくなります。そのような情報が外部から送信された場合に、エージェントでフィルターがかかるからです。
>
>Web サーバーを経由せずに AEM インスタンスに直接アクセスできるユーザーは、別の既知のユーザーのヘッダー、cookie またはパラメーターを送信することで、そのユーザーとして行動できます。
>
>ヘッダー、cookie および要求パラメーターの名前についても、SSO 設定で必要となるものだけを設定するようにしてください。

>[!NOTE]
>
>シングルサインオンは、多くの場合、[LDAP](/help/sites-administering/ldap-config.md) と共に使用されます。

>[!NOTE]
>
>Microsoft Internet Information Server（IIS）と共に [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) も使用している場合は、以下で追加の設定を行う必要があります。
>
>* `disp_iis.ini`
>* IIS

>
>`disp_iis.ini` で次のように設定します。
> （詳しくは、[Dispatcher を Microsoft Internet Information Server と共にインストールする方法に関するページ](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server)を参照してください）
>
>* `servervariables=1`（IIS サーバー変数をリクエストヘッダーとしてリモートインスタンスに転送します）
>* `replaceauthorization=1`（「Basic」を除く、「Authorization」という名前のすべてのヘッダーを「Basic」と同等のものに置き換えます）

>
>IIS では、次のように設定します。
>
>* **匿名アクセス**&#x200B;を無効にする
>
>* **統合 Windows 認証**&#x200B;を有効にします。

>


Felix コンソールの「**Authenticator**」オプションを使用すると、コンテンツツリーのすべてのセクションに適用される認証ハンドラーを確認できます。次に例を示します。

`http://localhost:4502/system/console/slingauth`

パスに最適なハンドラーが最初に照会されます。例えば、パス `/` に handler-A を設定し、パス `/content` に handler-B を設定すると、`/content/mypage.html` へのリクエストに対して handler-B が最初に照会されます。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 例 {#example}

cookie リクエスト（URL `http://localhost:4502/libs/wcm/content/siteadmin.html` を使用）の例を次に示します。

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

次の設定を使用します。

* **パス**：`/`

* **ヘッダー名**：`TestHeader`

* **cookie 名**：`TestCookie`

* **パラメーター名**：`TestParameter`

* **ID 形式**：`AsIs`

応答は次のようになります。

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

これは、次をリクエストした場合にも機能します。
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

または、次の curl コマンドを使用して、`TestHeader` ヘッダーを `admin:` に送信します
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>ブラウザーで要求パラメーターを使用したときは、HTML の一部だけが（CSS なしで）表示されます。これは、HTML からの要求はすべて要求パラメーターなしでおこなわれるからです。

## AEM サインアウトリンクの削除 {#removing-aem-sign-out-links}

SSO を使用する場合、サインインとサインアウトは外部で処理されるので、AEM 独自のサインアウトリンクは不要であり、削除する必要があります。

ようこそ画面のサインアウトリンクは以下の手順で削除できます。

1. `/libs/cq/core/components/welcome/welcome.jsp` を `/apps/cq/core/components/welcome/welcome.jsp` にオーバーレイします
1. jsp の以下の部分を削除します。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

右上隅にあるユーザーの個人メニューのサインアウトリンクを削除するには、以下の手順を実行します。

1. `/libs/cq/ui/widgets/source/widgets/UserInfo.js` を `/apps/cq/ui/widgets/source/widgets/UserInfo.js` にオーバーレイします

1. ファイルの以下の部分を削除します。

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
