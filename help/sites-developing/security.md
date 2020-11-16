---
title: セキュリティ
seo-title: セキュリティ
description: アプリケーションのセキュリティは、開発フェーズから始まります
seo-description: アプリケーションのセキュリティは、開発フェーズから始まります
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 66%

---


# セキュリティ{#security}

アプリケーションのセキュリティは、開発フェーズから始まります。アドビでは、次のセキュリティベストプラクティスを実施することをお勧めします。

## リクエストセッションの使用 {#use-request-session}

leas権限の原則に従い、Adobeでは、すべてのリポジトリアクセスは、ユーザー要求と適切なアクセス制御にバインドされたセッションを使用して行うことを推奨します。

## クロスサイトスクリプティング（XSS）に対する保護{#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング（XSS）を利用することにより、攻撃者は他のユーザーが表示する Web ページにコードを埋め込むことができます。このセキュリティ脆弱性が悪意のある Web ユーザーに悪用され、アクセス制御が擦り抜けられる可能性があります。

AEM では、ユーザーが提供するコンテンツをすべて出力時にフィルタリングする原則を適用しています。XSS を回避することは、開発時にもテスト時にも第一優先となります。

AEMが提供するXSS保護メカニズムは、 [OWASP(The OpenWeb アプリケーションセキュリティプロジェクト)が提供するAntiSamy Java Library](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ( [AntiSamy Java Library](https://www.owasp.org/))に基づいています。 デフォルトのAntiSamy設定は、次を参照してください。

`/libs/cq/xssprotection/config.xml`

この設定を、設定ファイルをオーバーレイすることで、独自のセキュリティニーズに合わせて調整することが重要です。 セキュリティ要件を実装するために必要な情報は、 [AntiSamyの公式ドキュメント](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に記載されています。

>[!NOTE]
>
>XSS 対策 API にアクセスする場合は、[AEM が提供する XSSAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html) を常に使用することを強くお勧めします。

Additionally, a web application firewall, such as [mod_security for Apache](https://www.modsecurity.org), can provide reliable, central control over the security of the deployment environment and protect against previously undetected cross-site scripting attacks.

## クラウドサービス情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なクラウドサービス情報用の ACL と OSGi 設定は、[実稼動準備モード](/help/sites-administering/production-ready.md)の一部として自動化されます。つまり、設定の変更を手動で行う必要はありませんが、デプロイメントの運用を開始する前に変更を確認しておくことをお勧めします。

[AEM インスタンスを Adobe Marketing Cloud と統合する](/help/sites-administering/marketing-cloud.md)場合は、[クラウドサービス設定](/help/sites-developing/extending-cloud-config.md)を使用します。これらの設定に関する情報は、収集された統計と共にリポジトリに格納されます。この機能を使用する場合は、この情報に適用されるデフォルトのセキュリティが要件に対応しているかどうかを確認することをお勧めします。

webservicesupport モジュールは、統計と設定情報を次の場所に書き込みます。

`/etc/cloudservices`

デフォルトの権限では、次の処理が可能です。

* 作成者環境: `read` for `contributors`

* 発行環境: `read` for `everyone`

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) および [CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。