---
title: 証明書失効リストの管理
description: 証明書失効リストを管理する方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 6%

---

# 証明書失効リストの管理{#managing-certificate-revocationlists}

Trust Store の管理を使用して、証明書失効リスト (CRL) の読み込み、編集および削除を行うことができます。 Base64 および DER でエンコードされた証明書失効リストがサポートされています。

## CRL の読み込み {#import-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックし、「読み込み」をクリックします。
1. 「エイリアス」ボックスに、CRL の識別子を入力します。
1. 「参照」をクリックして CRL を探し、「OK」をクリックします。

## CRL の書き出し {#export-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックします。
1. 書き出し可能な CRL のエイリアス名をクリックし、「書き出し」をクリックします。
1. 指示に従って、CRL を書き出すことができます。 CRL は Base64 エンコーディングで書き出されます。
1. 「OK」をクリックします。

## CRL の削除 {#delete-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックします。
1. 削除する CRL のチェックボックスをオンにし、「削除」をクリックして、「OK」をクリックします。
