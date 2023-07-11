---
title: セキュリティ
description: 開発フェーズ中にアプリケーションのセキュリティが開始
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 22%

---

# セキュリティ{#security}

アプリケーションのセキュリティは、開発フェーズで開始します。 Adobeでは、次のセキュリティのベストプラクティスを適用することをお勧めします。

## リクエストセッションを使用 {#use-request-session}

最小権限の原則に従って、アドビでは、リポジトリへのすべてのアクセスを、ユーザー要求と適切なアクセス制御にバインドされたセッションを使用して行うことをお勧めします。

## クロスサイトスクリプティング (XSS) に対するProtect {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング (XSS) を使用すると、攻撃者は他のユーザーが閲覧した Web ページにコードを挿入できます。 このセキュリティ脆弱性は、悪意のある Web ユーザーによって悪用され、アクセス制御をバイパスする可能性があります。

AEMは、ユーザーが指定したすべてのコンテンツを出力時にフィルタリングする原則を適用します。 開発とテストの両方で、XSS の防止が最も優先されます。

AEMが提供する XSS 保護メカニズムは、 [AntiSamy Java™ライブラリ](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供： [OWASP(Open Web Application Security Project)](https://owasp.org/).デフォルトの AntiSamy 設定は、次の場所にあります。

`/libs/cq/xssprotection/config.xml`

設定ファイルをオーバーレイすることで、この設定を独自のセキュリティ要件に適合させることが重要です。役人は [AntiSamy ドキュメント](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) は、セキュリティ要件を実装するために必要なすべての情報を提供します。

>[!NOTE]
>
>Adobeでは、常に [AEMが提供する XSSAPI](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

また、Web アプリケーションファイアウォール ( [Apache 向け mod_security](https://www.modsecurity.org)を使用すると、デプロイメント環境のセキュリティを一元的に確実に制御し、未検出のクロスサイトスクリプティング攻撃から保護できます。

## Cloud Service情報へのアクセス {#access-to-cloud-service-information}

>[!NOTE]
>
>インスタンスの保護に必要なCloud Service情報の ACL と OSGi 設定は、 [実稼動準備モード](/help/sites-administering/production-ready.md). つまり、設定を手動で変更する必要はありませんが、デプロイメントの運用を開始する前に設定を確認することをお勧めします。

次の場合： [AEMインスタンスとAdobe Experience Cloudの統合](/help/sites-administering/marketing-cloud.md)、 [Cloud Service設定](/help/sites-developing/extending-cloud-config.md). これらの設定に関する情報は、収集された統計と共にリポジトリに保存されます。 Adobeでは、この機能を使用する場合、この情報に対するデフォルトのセキュリティが要件を満たしているかどうかを確認することをお勧めします。

webservicesupport モジュールは、次の場所に統計情報と設定情報を書き込みます。

`/etc/cloudservices`

デフォルトの権限は、次のとおりです。

* オーサー環境：`contributors` に対する `read` 権限

* パブリッシュ環境：`everyone` に対する `read` 権限

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protect-against-cross-site-request-forgery-attacks}

CSRF 攻撃を軽減するために AEM で採用されているセキュリティメカニズムについて詳しくは、セキュリティチェックリストの [Sling リファラーフィルター](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)の節と、[CSRF 対策フレームワークのドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。
