---
title: 証明書と資格情報の管理の基本事項
description: 証明書と資格情報の管理の基本事項について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 100%

---

# 証明書と資格情報の管理の基本事項 {#basics-of-managing-certificates-and-credentials}

*資格情報*&#x200B;には、ドキュメントへの署名や識別に必要な秘密鍵情報が格納されています。*証明書*&#x200B;は、信頼のために設定する公開鍵情報です。AEM Forms が証明書と資格情報を使用する目的はいくつかあります。

* Acrobat Reader DC Extensions では、資格情報を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。（[証明書を Acrobat Reader DC Extensions で使用するための設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)を参照）。
* Acrobat での使用を目的として、信頼された発行者からの秘密鍵証明書のみを表示するように Rights Management を設定できます（[Rights Management の表示設定の指定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)を参照）。証明書には共通名（CN）が存在する必要があります。
* Signature サービスは、証明書と資格情報にアクセスします。Signature サービスについて詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_65_jp)を参照してください。

**ペアとなる鍵の生成**

AEM Forms では、Trust Store を使用して、証明書、資格情報および証明書失効リスト（CRL）を保存および管理します。また、独立したハードウェアセキュリティモジュール（HSM）デバイスを使用して、秘密鍵を保存できます。

AEM Forms では、キーペアを生成するためのオプションは提供されません。ただし、Java keytool などのツールを使用してキーペアを生成し、AEM Forms Trust Store に読み込むことができます。Java keytool について詳しくは、次の記事を参照してください。

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

次の署名タイプは AEM Forms でサポートされ、読み込むことができます。

* XML 署名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 署名

**キーの消失、またはキーに問題が生じた場合の処理**

キーの消失、またはキーに問題が生じた可能性がある場合は次のように対応してください。

1. 認証機関に通知すると、認証機関は証明書失効リストに問題が発生したキーを追加し、このキーを失効させます。
1. 認証機関から新しいキーと証明書を取得します。
1. 問題のあったキーを使用して署名したドキュメントに、新しいキーを使用して再度署名します。
