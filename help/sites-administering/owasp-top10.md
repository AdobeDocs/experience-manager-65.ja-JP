---
title: OWASP Top 10
seo-title: OWASP Top 10
description: AEM で OWASP Top 10 のセキュリティリスクに対処する方法について説明します。
seo-description: AEM で OWASP Top 10 のセキュリティリスクに対処する方法について説明します。
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: cd7331f5f57ec90ea72d41d467891dc832347a3c
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 88%

---


# OWASP Top 10{#owasp-top}

[Open Web Application Security Project](https://www.owasp.org)（OWASP）は、[Top 10 Web Application Security Risks](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)（Web アプリケーションに関する上位 10 件のセキュリティリスク）のリストを保持しています。

これらのリスクおよび CRX での対処方法を以下に示します。

## 1. インジェクション {#injection}

* SQL - 設計により防止されます。デフォルトのリポジトリ設定には従来のデータベースが含まれず、また必要でもありません。データはすべてコンテンツリポジトリに格納されます。すべてのアクセスは認証されたユーザーに制限され、JCR API を使用してのみ実行可能です。SQL は検索クエリ（SELECT）のみをサポートします。さらに、SQL は値バインディングをサポートします。
* LDAP - 認証モジュールによって入力にフィルターが適用され、バインドメソッドを使用してユーザーの読み込みが実行されるので、LDAP インジェクションは不可能です。
* OS - アプリケーション内からのシェル実行はありません。

## 2. クロスサイトスクリプティング（XSS） {#cross-site-scripting-xss}

このリスクを軽減する一般的な方法は、[OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) と [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に基づくサーバー側の XSS 保護ライブラリを使用して、ユーザーが生成したコンテンツのすべての出力をエンコードすることです。

XSS はテスト時および開発時における最優先事項であり、検出された問題は（通常）すぐに解決されます。

## 3. 認証とセッション管理の不備 {#broken-authentication-and-session-management}

AEM では、[Apache Jackrabbit](https://jackrabbit.apache.org/) と [Apache Sling](https://sling.apache.org/) に基づく、堅実で実績のある認証手法を利用しています。ブラウザー／HTTP セッションは AEM では使用されません。

## 4. 安全でないオブジェクト直接参照 {#insecure-direct-object-references}

データオブジェクトへのすべてのアクセスは、リポジトリが介在するので、役割に基づくアクセス制御によって制限されます。

## 5. クロスサイトリクエストフォージェリ（CSRF） {#cross-site-request-forgery-csrf}

クロスサイト要求偽造(CSRF)は、すべてのフォームとAJAXリクエストに暗号化トークンを自動的に挿入し、各POSTに対してサーバー上でこのトークンを検証することで軽減されます。

In addition, AEM ships with a referrer-header based filter, which can be configured to *only* allow POST requests from specific hosts (defined in a list).

## 6. セキュリティ設定のミス {#security-misconfiguration}

すべてのソフトウェアを常に正しく設定した状態にしておくことは不可能です。しかし、アドビでは、できるだけ多くのガイダンスを提供し、設定をできるだけシンプルにするよう努めています。さらに、AEM に搭載されている[セキュリティヘルスチェック機能](/help/sites-administering/operations-dashboard.md)により、一目でセキュリティ設定を監視できます。

詳しくは、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。セキュリティ強化の手順を段階的に説明します。

## 7. 安全でない暗号化データの保管 {#insecure-cryptographic-storage}

パスワードは暗号化ハッシュとしてユーザーノードに格納されます。デフォルトでは、このようなノードは管理者とユーザー自身だけが確認できます。

サードパーティの資格情報などのような重要な情報は、FIPS 140-2 認定を受けた暗号ライブラリを使用して、暗号化された形式で保存されます。

## 8. URL アクセス制限の失敗 {#failure-to-restrict-url-access}

リポジトリでは、アクセス制御エントリを使用して、特定のパスの特定のユーザーまたはグループに対して[（JCR で指定された）詳細な権限](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)を設定できます。アクセス制限はリポジトリによって適用されます。

## 9. 不十分なトランスポート層の保護 {#insufficient-transport-layer-protection}

サーバー設定（例：HTTPS のみの使用）によって軽減されます。

## 10. 未検証のリダイレクトとフォワード {#unvalidated-redirects-and-forwards}

ユーザーが指定した宛先へのすべてのリダイレクトを内部の場所に制限することで軽減されます。

