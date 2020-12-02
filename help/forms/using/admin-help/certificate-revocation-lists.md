---
title: 証明書失効リストの管理
seo-title: 証明書失効リストの管理
description: 証明書失効リストの管理方法について説明します。
seo-description: 証明書失効リストの管理方法について説明します。
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 100%

---


# 証明書失効リストの管理{#managing-certificate-revocationlists}

Trust Store の管理では、証明書失効リスト（CRL）の読み込み、編集および削除を行うことができます。Base64 および DER でエンコードされた証明書失効リストがサポートされます。

## CRL の読み込み  {#import-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックして、「読み込み」をクリックします。
1. 「エイリアス」ボックスに、CRL の ID を入力します。
1. 「参照」をクリックして CRL を見つけ、「OK」をクリックします。

## CRL の書き出し  {#export-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 書き出す CRL のエイリアス名をクリックし、「書き出し」をクリックします。
1. 指示に従って CRL を書き出します。CRL は Base64 エンコードで書き出されます。
1. 「OK」をクリックします。

## CRL の削除  {#delete-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 削除する CRL のチェックボックスをオンにして「削除」をクリックし、「OK」をクリックします。

