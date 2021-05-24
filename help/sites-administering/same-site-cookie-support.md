---
title: AEM 6.5に対する同じサイトのcookieのサポート
description: AEM 6.5に対する同じサイトのcookieのサポート
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 69%

---

# AEM 6.5での同じサイトのcookieのサポート{#same-site-cookie-support-for-aem-65}

バージョン 80 以降、Chrome およびそれ以降の Safari では、cookie セキュリティの新しいモデルが導入されました。このモードは、`SameSite`と呼ばれる設定を通じて、サードパーティサイトにCookieの可用性に関するセキュリティ制御を導入するように設計されています。 詳しくは、こちらの[記事](https://web.dev/samesite-cookies-explained/)を参照してください。

この設定のデフォルト値（`SameSite=Lax`）により、AEM インスタンスまたはサービス間の認証が機能しないことがあります。これは、これらのサービスのドメインや URL 構造が、この cookie ポリシーの制約に該当しない可能性があるためです。

この問題を回避するには、ログイントークンのSameSite cookieを`None`に設定する必要があります。

これは、次の手順でおこなえます。

1. Web コンソール（`http://serveraddress:serverport/system/console/configMgr`）にアクセスします。
1. **Adobe Granite Token Authentication Handler** を検索してクリックします。
1. 次の図に示すように、**login-token cookie の SameSite 属性**&#x200B;を `None` に設定します。
   ![samesite](assets/samesite1.png)
1. 「保存」をクリックします。
1. この設定が更新され、ユーザーがログアウトしてから再度ログインすると、`login-token` cookieに `None` 属性が設定され、クロスサイトリクエストに含められるようになります。
