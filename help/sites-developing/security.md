---
title: セキュリティ
seo-title: Security
description: アプリケーションのセキュリティは、開発フェーズから始まります
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: ht
source-wordcount: '426'
ht-degree: 100%

---

# セキュリティ{#security}

アプリケーションのセキュリティは、開発フェーズから始まります。アドビでは、次のセキュリティベストプラクティスを実施することをお勧めします。

## リクエストセッションの使用 {#use-request-session}

最小権限の原則に従って、アドビでは、リポジトリへのすべてのアクセスを、ユーザー要求と適切なアクセス制御にバインドされたセッションを使用して行うことをお勧めします。

## クロスサイトスクリプティング（XSS）に対する保護 {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング（XSS）を利用することにより、攻撃者は他のユーザーが表示する Web ページにコードを埋め込むことができます。このセキュリティ脆弱性が悪意のある Web ユーザーに悪用され、アクセス制御が擦り抜けられる可能性があります。

AEM では、ユーザーが提供するコンテンツをすべて出力時にフィルタリングする原則を適用しています。XSS を回避することは、開発時にもテスト時にも第一優先となります。

AEM が提供する XSS 保護メカニズムは、[OWASP（The Open Web Application Security Project）](https://www.owasp.org/)が提供する [AntiSamy Java ライブラリ](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)に基づいています。デフォルトの AntiSamy 構成は、次の場所にあります。

`/libs/cq/xssprotection/config.xml`

設定ファイルをオーバーレイすることで、この設定を独自のセキュリティ要件に適合させることが重要です。公式の [AntiSamy ドキュメント](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)では、セキュリティ要件を実装するために必要なすべての情報が提供されています。

>[!NOTE]
>
>[AEM が提供する XSSAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html) を使用して、常に XSS 対策 API にアクセスすることを強くお勧めします。

また、[Apache 対応の mod_security](https://www.modsecurity.org) などの web アプリケーションファイアウォールを使用すると、デプロイメント環境のセキュリティを高い信頼性で一元的に制御でき、以前は検出されなかったクロスサイトスクリプティング攻撃に対する保護も可能になります。

## クラウドサービス情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なクラウドサービス情報用の ACL と OSGi 設定は、[実稼動準備モード](/help/sites-administering/production-ready.md)の一部として自動化されます。つまり、設定の変更を手動で行う必要はありませんが、設定されていることをデプロイメントの運用を開始する前に確認しておくことをお勧めします。

[AEM インスタンスを Adobe Marketing Cloud と統合する](/help/sites-administering/marketing-cloud.md)場合は、[クラウドサービス設定](/help/sites-developing/extending-cloud-config.md)を使用します。これらの設定に関する情報は、収集された統計と共にリポジトリに格納されます。この機能を使用する場合は、この情報に適用されるデフォルトのセキュリティが要件に対応しているかどうかを確認することをお勧めします。

webservicesupport モジュールは、統計と設定情報を次の場所に書き込みます。

`/etc/cloudservices`

デフォルトの権限は、次のとおりです。

* オーサー環境：`contributors` に対する `read` 権限

* パブリッシュ環境：`everyone` に対する `read` 権限

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling リファラーフィルター](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)の節と、[CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。
