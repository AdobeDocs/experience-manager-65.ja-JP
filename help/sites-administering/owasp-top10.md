---
title: OWASP Top 10
description: AEMが OWASP の上位 10 のセキュリティリスクにどのように対処するかを説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 33%

---

# OWASP Top 10{#owasp-top}

この [Web アプリケーションセキュリティプロジェクトを開く](https://owasp.org/) （OWASP）は、 [上位 10 件の Web アプリケーションのセキュリティ リスク](https://owasp.org/www-project-top-ten/).

これらは以下に示され、CRX での処理方法についても説明されています。

## 1.インジェクション {#injection}

* SQL - デザインにより防止：デフォルトのリポジトリ設定には、従来のデータベースが含まれていることも必要もありません。すべてのデータはコンテンツリポジトリに保存されます。 すべてのアクセスは、認証済みユーザーに限定され、JCR API 経由でのみ実行できます。 SQL は検索クエリでのみサポートされています（SELECT）。 さらに、SQL は値バインディングをサポートします。
* LDAP – 認証モジュールが入力をフィルタリングし、bind メソッドを使用してユーザーのインポートを実行するので、LDAP の挿入は使用できません。
* OS - アプリケーション内から実行されるシェルはありません。

## 2. クロスサイトスクリプティング（XSS） {#cross-site-scripting-xss}

このリスクを軽減する一般的な方法は、[OWASP Encoder](https://owasp.org/www-project-java-encoder/) と [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に基づくサーバー側の XSS 保護ライブラリを使用して、ユーザーが生成したコンテンツのすべての出力をエンコードすることです。

XSS はテスト時および開発時における最優先事項であり、検出された問題は（通常）すぐに解決されます。

## 3. 認証とセッション管理の不備 {#broken-authentication-and-session-management}

AEM では、[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) と [Apache Sling](https://sling.apache.org/) に基づく、堅実で実績のある認証手法を利用しています。ブラウザー／HTTP セッションは AEM では使用されません。

## 4.安全でない直接オブジェクト参照 {#insecure-direct-object-references}

データオブジェクトへのすべてのアクセスはリポジトリによって仲介されるので、役割ベースのアクセス制御によって制限されます。

## 5. クロスサイトリクエストフォージェリ（CSRF） {#cross-site-request-forgery-csrf}

クロスサイトリクエストフォージェリ（CSRF）は、暗号トークンをあらゆる形式および AJAX リクエストに自動的に注入し、すべての POST についてこのトークンをサーバー上で検証することで軽減されます。

さらに、AEM に搭載されているリファラーヘッダーベースのフィルターを設定して、特定のホスト（リストで定義）からの POST リクエスト&#x200B;*のみ*&#x200B;を許可することができます。

## 6. セキュリティの設定ミス {#security-misconfiguration}

すべてのソフトウェアが常に正しく設定されていることを保証することは不可能です。 ただし、Adobeは、可能な限り多くのガイダンスを提供し、設定をできる限り簡単にするよう努めています。 さらに、AEMには次の製品が付属しています [統合セキュリティヘルスチェック](/help/sites-administering/operations-dashboard.md) セキュリティ設定を一目で監視するのに役立ちます。

をレビュー [セキュリティチェックリスト](/help/sites-administering/security-checklist.md) 詳しくは、ステップバイステップの堅牢化手順を参照してください。

## 7.安全でない暗号化ストレージ {#insecure-cryptographic-storage}

パスワードは、暗号化ハッシュとしてユーザーノードに保存されます。 デフォルトでは、このようなノードは、管理者およびユーザー自身のみが読み取ることができます。

サードパーティの資格情報などの機密データは、FIPS 140-2 認定暗号化ライブラリを使用して、暗号化された形式で保存されます。

## 8. URL アクセスの制限の失敗 {#failure-to-restrict-url-access}

リポジトリでは、次の設定が可能です [詳細な権限（JCR で指定されたもの）](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) アクセス制御エントリを使用して、特定のパスの特定のユーザーまたはグループに対して実行します。 アクセス制限はリポジトリによって適用されます。

## 9. 不十分なトランスポート層の保護 {#insufficient-transport-layer-protection}

サーバー設定によって軽減されます（例えば、HTTPS のみを使用）。

## 10. 未検証のリダイレクトとフォワード {#unvalidated-redirects-and-forwards}

ユーザーが指定した宛先へのすべてのリダイレクトを内部の場所に制限することで軽減されます。
