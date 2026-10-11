---
title: セキュリティ
description: アプリケーションのセキュリティは、開発フェーズから始まります。
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 96%
---
# セキュリティ{#security}

アプリケーションのセキュリティは、開発フェーズから始まります。 アドビでは、次のセキュリティのベストプラクティスを適用することをお勧めします。

## リクエストセッションの使用 {#use-request-session}

最小権限の原則に従って、アドビでは、リポジトリへのすべてのアクセスを、ユーザー要求と適切なアクセス制御にバインドされたセッションを使用して行うことをお勧めします。

## クロスサイトスクリプティング（XSS）に対する保護 {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング（XSS）を使用すると、攻撃者が他のユーザーが閲覧した web ページにコードを挿入できます。 このセキュリティ脆弱性は、悪意のある web ユーザーによって悪用され、アクセス制御をバイパスする可能性があります。

AEM では、ユーザーが提供するコンテンツをすべて出力時にフィルタリングする原則を適用しています。 XSS を回避することは、開発とテストの両方において最優先されます。

AEM が提供する XSS 保護メカニズムは、[OWASP（The Open Web Application Security Project）](https://owasp.org/)が提供する [AntiSamy Java™ ライブラリ](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)に基づいています。 デフォルトの AntiSamy 設定は、次の場所にあります。

`/libs/cq/xssprotection/config.xml`

設定ファイルをオーバーレイすることで、この設定を独自のセキュリティ要件に適合させることが重要です。 公式の [AntiSamy ドキュメント](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)では、セキュリティ要件の実装に必要なすべての情報が提供されています。

>[!NOTE]
>
>アドビでは、[AEM が提供する XSSAPI](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html) を使用して、常に XSS Protection API にアクセスすることをお勧めします。

また、[Apache 対応の mod_security](https://www.modsecurity.org) などの web アプリケーションファイアウォールを使用すると、デプロイメント環境のセキュリティを高い信頼性で一元的に制御でき、以前は検出されなかったクロスサイトスクリプティング攻撃に対する保護も可能です。

## クラウドサービス情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なクラウドサービス情報用の ACL と OSGi 設定は、[実稼動準備モード](/help/sites-administering/production-ready.md)の一部として自動化されます。 つまり、設定を手動で変更する必要はありませんが、デプロイメントの運用を開始する前に変更を確認しておくことをお勧めします。

[AEM インスタンスを Adobe Experience Cloud と統合](/help/sites-administering/marketing-cloud.md)する場合、[クラウドサービス設定](/help/sites-developing/extending-cloud-config.md)を使用します。 これらの設定に関する情報は、収集された統計と共にリポジトリに保存されます。 アドビでは、この機能を使用している場合、この情報に対するデフォルトのセキュリティが要件を満たしているかどうかを確認することをお勧めします。

webservicesupport モジュールは、統計情報と設定情報を以下に書き込みます。

`/etc/cloudservices`

デフォルトの権限は、次のとおりです。

* オーサー環境：`contributors` に対する `read` 権限

* パブリッシュ環境：`everyone` に対する `read` 権限

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling リファラーフィルター](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)の節と、[CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。
