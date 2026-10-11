---
title: OWASP Top 10
description: AEM で OWASP Top 10 のセキュリティリスクに対処する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 86%
---
# OWASP Top 10{#owasp-top}

[Open Web Application Security Project](https://owasp.org/)（OWASP）は、[Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/)（Web アプリケーションに関する上位 10 件のセキュリティリスク）のリストを保持しています。

これらのリスクおよび CRX での対処方法を以下に示します。

## &#x200B;1. 注射 {#injection}

* SQL - 設計により防止されます。デフォルトのリポジトリ設定には従来のデータベースが含まれず、また必要でもありません。データはすべてコンテンツリポジトリに格納されます。 すべてのアクセスは認証されたユーザーに制限され、JCR API を介してのみ実行可能です。 SQL は検索クエリ（SELECT）のみをサポートします。 さらに、SQL は値バインディングをサポートします。
* LDAP - 認証モジュールによって入力にフィルターが適用され、バインドメソッドを使用してユーザーの読み込みが実行されるので、LDAP インジェクションは不可能です。
* OS - アプリケーション内からのシェル実行はありません。

## &#x200B;2. クロスサイトスクリプティング（XSS） {#cross-site-scripting-xss}

このリスクを軽減する一般的な方法は、[OWASP Encoder](https://owasp.org/www-project-java-encoder/) と [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に基づくサーバー側の XSS 保護ライブラリを使用して、ユーザーが生成したコンテンツのすべての出力をエンコードすることです。

XSS はテスト時および開発時における最優先事項であり、検出された問題は（通常）すぐに解決されます。

## &#x200B;3. ブロークン認証とセッション管理 {#broken-authentication-and-session-management}

AEMでは、[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html)および[Apache Sling](https://sling.apache.org/)を利用して、サウンドおよび実証済みの認証手法を使用しています。 Browser/HTTP Sessionsは、AEMでは使用されません。

## &#x200B;4. 安全でないダイレクトオブジェクト参照 {#insecure-direct-object-references}

データオブジェクトへのすべてのアクセスは、リポジトリが介在するので、役割に基づくアクセス制御によって制限されます。

## &#x200B;5. クロスサイトリクエストフォージェリー（CSRF） {#cross-site-request-forgery-csrf}

クロスサイトリクエストフォージェリ（CSRF）は、暗号トークンをあらゆる形式および AJAX リクエストに自動的に注入し、すべての POST についてこのトークンをサーバー上で検証することで軽減されます。

さらに、AEM に搭載されているリファラーヘッダーベースのフィルターを設定して、特定のホスト（リストで定義）からの POST リクエスト&#x200B;*のみ*&#x200B;を許可することができます。

## &#x200B;6. セキュリティ設定ミス {#security-misconfiguration}

すべてのソフトウェアを常に正しく設定した状態にしておくことは不可能です。 しかし、アドビでは、できるだけ多くのガイダンスを提供し、設定をできるだけシンプルにするよう努めています。 さらに、AEM に搭載されている[セキュリティヘルスチェック機能](/help/sites-administering/operations-dashboard.md)により、一目でセキュリティ設定を監視できます。

詳しくは、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。セキュリティ強化の手順を段階的に説明します。

## &#x200B;7. 安全でない暗号化ストレージ {#insecure-cryptographic-storage}

パスワードは暗号化ハッシュとしてユーザーノードに格納されます。 デフォルトでは、このようなノードは管理者とユーザー自身だけが確認できます。

サードパーティの資格情報などのような重要な情報は、FIPS 140-2 認定を受けた暗号ライブラリを使用して、暗号化された形式で保存されます。

## &#x200B;8. URL アクセス制限の失敗 {#failure-to-restrict-url-access}

リポジトリでは、アクセス制御エントリを使用して、特定のパスの特定のユーザーまたはグループに対して[（JCR で指定された）詳細な権限](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/jcr/2.0/16_Access_Control_Management.html)を設定できます。 アクセス制限はリポジトリによって適用されます。

## &#x200B;9. トランスポート層の保護が不十分 {#insufficient-transport-layer-protection}

サーバー設定（例：HTTPS のみの使用）によって軽減されます。

## &#x200B;10. 未検証のリダイレクトと転送 {#unvalidated-redirects-and-forwards}

ユーザーが指定した宛先へのすべてのリダイレクトを内部の場所に制限することで軽減されます。
