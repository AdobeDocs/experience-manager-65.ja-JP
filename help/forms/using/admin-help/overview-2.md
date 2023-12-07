---
title: 証明書と資格情報の管理の基本事項
description: 証明書と資格情報の管理の基本について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 11%

---

# 証明書と資格情報の管理の基本事項 {#basics-of-managing-certificates-and-credentials}

A *資格情報* には、ドキュメントの署名や識別に必要な秘密鍵情報が含まれます。 A *証明書* は、信頼用に設定する公開鍵情報です。 AEM forms では、いくつかの目的で証明書と秘密鍵証明書を使用します。

* Acrobat Reader DC Extensions では、資格情報を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。( 詳しくは、 [Acrobat Reader DC Extensions で使用するための資格情報の設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Acrobatで使用するRights Management情報を、信頼できる発行者からのみ表示するように設定できます。 ( 詳しくは、 [Rights Managementの表示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) 証明書に共通名 (CN) が存在する必要があります。
* Signature サービスは証明書と資格情報にアクセスします。 Signature サービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_65_jp).

**ペアキーの生成**

AEM forms では、Trust Store を使用して、証明書、秘密鍵証明書および証明書失効リスト (CRL) を保存および管理します。 また、独立したハードウェアセキュリティモジュール (HSM) デバイスを使用して、秘密鍵を保存することもできます。

AEM forms には、キーペアを生成するオプションはありません。 ただし、Java keytool などのツールを使用して生成し、AEM forms Trust Store に読み込むことができます。 Java keytool について詳しくは、次を参照してください。

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

次の署名タイプがサポートされ、AEM forms で読み込むことができます。

* XML 署名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 署名

**キーの紛失または改ざんの処理**

鍵が失われた、または鍵が侵害されたと思われる場合は、次の操作を行ってください。

1. 認証局に通知して、認証失効リストに問題が発生したキーを追加し、キーを失効させます。
1. 認証機関から新しいキーと証明書を取得します。
1. 問題が発生したキーを使用して署名したドキュメントに、新しいキーを使用して再び署名します。
