---
title: LDAP バインドパスワードの設定
description: 設定ファイルを別のシステムに読み込む前に、バインドパスワードフィールドを設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 100%

---

# LDAP バインドパスワードの設定{#configure-the-ldap-bind-password}

セキュリティ上の問題を防ぐため、書き出された設定ファイル（config.xml）のバインドパスワードフィールドは設定されていません。設定ファイルを別のシステムに読み込む前に、このパスワードを設定してください。このパスワードは、データベースに格納されている既存のパスワードを上書きします。パスワードが null の場合は、既存の null 以外のパスワード値は上書きされません。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. ファイルに現在の設定をエクスポートするには、「エクスポート」をクリックして別の場所に設定ファイルを保存します。
1. ファイル内で、`Domains`／*[自分のドメイン名]*／`DirectoryConfigs`／`LDAPGroupConfig` ノードを探します。次は例です。

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   `bindpassword` の値を入力して変更を保存します。

1. ファイル内で、`Domains`／*[自分のドメイン名]*／`DirectoryConfigs`／`LDAPGroupConfig`／`LDAPUserConfig` ノードを探します。次は例です。

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   `bindpassword` の値を入力して変更を保存します。

1. 更新したファイルをインポートするには、User Management で、「設定ファイルのインポートとエクスポート」をクリックします。
1. 「参照」をクリックしてファイルを探し、「インポート」をクリックして「OK」をクリックします。
