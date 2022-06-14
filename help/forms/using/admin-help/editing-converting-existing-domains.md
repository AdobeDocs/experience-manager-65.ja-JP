---
title: 既存のドメインの編集と変換
seo-title: Editing and converting existing domains
description: ドメインの管理ページから既存のドメインの設定を変更する方法について説明します。既存のエンタープライズドメインをハイブリッドドメインに（またはその逆に）変換します。
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 100%

---

# 既存のドメインの編集と変換{#editing-and-converting-existing-domains}

ドメインの管理ページから既存のドメインの設定を変更できます。また、既存のエンタープライズドメインをハイブリッドドメインに変換することもできます。

## 既存のドメインの編集 {#edit-an-existing-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 編集するドメインの名前をクリックします。
1. ドメイン名を変更するには、「名前」ボックスのテキストを変更します。
1. エンタープライズドメインまたはハイブリッドドメインの認証情報を変更するには、ページの下部で目的の認証名をクリックします。認証を編集ページで、必要に応じて設定を変更します（[認証の設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)を参照）。
1. エンタープライズドメインのディレクトリ情報を変更するには、ページの下部で目的のディレクトリ名をクリックします。ディレクトリを編集ページで、必要に応じて設定を変更します（[ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)を参照）。
1. 変更が完了したら、「OK」をクリックします。

## エンタープライズドメインのハイブリッドドメインへの変換 {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 変換するエンタープライズドメインの名前をクリックします。
1. 「ハイブイリッドドメインに変換」をクリックします。
1. ユーザーおよびグループのデータとユーザーの認証に関して表示された情報を確認し、「OK」をクリックします。
1. ハイブリッドドメインの設定を編集し、「OK」をクリックします。

>[!NOTE]
>
>変換するエンタープライズドメインにディレクトリ設定が含まれていない場合、LDAP 認証の設定が失われます。

## ハイブリッドドメインのエンタープライズドメインへの変換 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 変換するハイブリッドドメインの名前をクリックします。
1. 「エンタープライズドメインに変換」をクリックします。
1. ユーザーおよびグループのデータとユーザーの認証に関して表示された情報を確認し、「OK」をクリックします。
1. 「ディレクトリを追加」をクリックし、必要なディレクトリ情報を設定します（[ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)を参照）。
