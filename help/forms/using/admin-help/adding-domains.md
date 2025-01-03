---
title: ドメインの追加
description: ドメインの管理設定を使用してエンタープライズドメイン、ローカルドメイン、またはハイブリッドドメインを追加する方法と、ドメイン名と ID に関する一般的な考慮事項について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 100%

---

# ドメインの追加 {#adding-domains}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

## エンタープライズドメインを追加 {#add-an-enterprise-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックします。
1. 「ID」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します（[ドメイン名および ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids)を参照）。
1. アカウントロックを有効にするかどうかを指定します（[アカウントロックの設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)を参照）。デフォルトでは、「アカウントロックを有効にする」が選択されています。
1. 「認証を追加」をクリックし、「認証プロバイダー」リストで、組織が使用している認証メカニズムに応じてプロバイダーを選択します。選択できる値は、「LDAP」、「Kerberos」、「SAML」または「カスタム」認証プロバイダーです。

   LDAP を選択すると、ディレクトリ設定で指定した LDAP サーバーを使用するか、異なる LDAP サーバーを選択して認証に使用することができます。異なるサーバーを選択する場合、ユーザーは両方の LDAP サーバーに存在する必要があります。

1. 必要な追加情報をページに入力します（[認証の設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)を参照）。
1. ディレクトリまたはカスタムのサービスプロバイダーインターフェイス（SPI）を追加します（[ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)を参照）。
1. 「完了」をクリックし、「OK」をクリックします。

エンタープライズドメインを作成したら、User Management でディレクトリを使用する前に、手動でディレクトリを同期するか、同期を行うトリガーを作成する必要があります。その後、必要に応じてディレクトリの同期スケジュールを設定したり、手動で同期を実行したりすることができます（[ディレクトリの同期](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories)を参照）。

## ローカルドメインを追加 {#add-a-local-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規ローカルドメイン」をクリックします。
1. 「ID」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します（[ドメイン名および ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids)を参照）。
1. アカウントロックを有効にするかどうかを指定して、「OK」をクリックします（[アカウントロックの設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)を参照）。デフォルトでは、「アカウントロックを有効にする」が選択されています。

## ハイブリッドドメインを追加 {#add-a-hybrid-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新しいハイブリッドドメイン」をクリックします。
1. 「ID」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します（[ドメイン名および ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids)を参照）。
1. 「認証を追加」をクリックし、「認証プロバイダー」リストで、組織が使用している認証メカニズムに応じてプロバイダーを選択します。選択できる値は、「LDAP」、「Kerberos」、「SAML」または「カスタム」認証プロバイダーです。
1. 必要な追加情報をページに入力します（[認証の設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)を参照）。
1. 「OK」をクリックし、「OK」を再度クリックします。

## ドメイン名および ID に関する重要な考慮事項 {#important-considerations-for-domain-names-and-ids}

ドメイン名および ID の選択時には、次の点を考慮してください。

### 一般的な考慮事項 {#general-considerations}

* DB2 以外のデータベースプロバイダーを使用している場合、ドメイン ID には、最大 50 バイトまで含めることができます。1 バイトの ASCII 文字を使用する場合、上限は 50 文字です。ドメイン ID にマルチバイト文字が含まれている場合、この上限は低くなります。例えば、ID に 3 バイト文字が含まれるドメインを作成した場合、上限は 16 文字です。また、4 バイト文字を含むドメインは作成できません。この上限を超えるドメイン ID を作成すると、AEM Forms が不安定な状態になります。この不安定な状態から回復するには、（このページ）[拡張文字またはマルチバイト文字を含むドメインの削除](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)を参照してください。
* AEM forms 内で作成できるエンタープライズドメインとローカルドメインの数は、各ドメイン ID の長さによって異なります。エンタープライズドメインまたはハイブリッドドメインを追加すると、User Management によって AEM Forms 設定ファイル（config.xml）の AuthProviders ノードの configInstance 文字列が更新されます。configInstance 文字列には、認証プロバイダーに関連付けられているすべてのドメインの絶対パスをコロン区切りで記載したリストが含まれます。この文字列のサイズの上限は 8,192 文字です。この上限に達すると、追加のドメインを作成できません。

### DB2 を使用する際の考慮事項 {#considerations-when-using-db2}

AEM Forms データベースに DB2 を使用する場合、ドメイン ID の許可される最大長は、使用する文字の種類によって異なります。

* 1 バイト文字（ASCII）で 100 文字（例えば、英語、フランス語またはドイツ語で使用されている文字）
* 2 バイト文字で 50 文字（例えば、中国語、日本語または韓国語で使用されている文字）
* 4 バイト文字で 25 文字（例えば、繁体字中国語で使用されている文字）

### MySQL を使用する際の考慮事項 {#considerations-when-using-mysql}

MySQL を AEM Forms データベースとして使用している場合、以下の制限があります。

* ドメイン ID とドメイン名には 1 バイト（ASCII）文字のみを使用します。拡張 ASCII 文字を使用すると、AEM Forms の動作が不安定になり、ドメインを削除しようとすると例外がスローされる場合があります。この不安定な状態から回復するには、（このページ）[拡張文字またはマルチバイト文字を含むドメインの削除](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)を参照してください。
* 同じ名前で、大文字／小文字が異なる 2 つのドメインを作成することはできません。例えば、「*adobe*」というドメインが既に存在する場合に「*Adobe*」というドメインを作成しようとすると、エラーが発生します。
* User Management では、拡張文字の使用においてのみ異なる 2 つのドメイン名を区別することはできません。例えば、「*abcde*」という名前のドメインと「*âbcdè*」という名前のドメインを作成した場合、これら 2 つは同じと見なされます。

### 拡張文字またはマルチバイト文字を含むドメインを削除 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)の説明に従って、設定ファイルを書き出します。
1. 設定ファイルを開き、Domains ノードの下で、name 属性が拡張文字またはマルチバイト文字を使用して作成されたドメインの名前と一致するノードを探します。そのドメインに関連するノード全体を削除します。
1. データベースで、edcprincipaldomainentity テーブル内のドメインを検索します。

   * edcprincipaldomainentity から `*` を選択します。
   * 拡張文字またはマルチバイト文字を含むドメイン名を検索し、そのステータスを廃止に設定します。

1. [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)の説明に従って、更新した設定ファイルを読み込みます。
