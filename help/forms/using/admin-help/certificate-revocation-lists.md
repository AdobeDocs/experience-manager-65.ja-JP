---
title: 証明書失効リストの管理
description: 証明書失効リストの管理方法について説明します。Trust Store の管理を使用して、証明書失効リスト（CRL）の読み込み、編集および削除を行うことができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 100%

---

# 証明書失効リストの管理{#managing-certificate-revocationlists}

Trust Store の管理では、証明書失効リスト（CRL）の読み込み、編集および削除を行うことができます。Base64 および DER でエンコードされた証明書失効リストがサポートされます。

## CRL を読み込み {#import-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックして、「読み込み」をクリックします。
1. 「エイリアス」ボックスに、CRL の ID を入力します。
1. 「参照」をクリックして CRL を見つけ、「OK」をクリックします。

## CRL を書き出し {#export-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 書き出す CRL のエイリアス名をクリックし、「書き出し」をクリックします。
1. 指示に従って CRL を書き出します。CRL は Base64 エンコードで書き出されます。
1. 「OK」をクリックします。

## CRL を削除 {#delete-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 削除する CRL のチェックボックスをオンにして「削除」をクリックし、「OK」をクリックします。
