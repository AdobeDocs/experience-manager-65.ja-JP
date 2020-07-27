---
title: LDAP バインドパスワードの設定
seo-title: LDAP バインドパスワードの設定
description: 設定ファイルを別のシステムに読み込む前にバインドパスワードを設定する方法について説明します。
seo-description: 設定ファイルを別のシステムに読み込む前にバインドパスワードを設定する方法について説明します。
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 91%

---


# LDAP バインドパスワードの設定{#configure-the-ldap-bind-password}

セキュリティ上の問題を防ぐため、書き出された設定ファイル（config.xml）のバインドパスワードフィールドは設定されていません。設定ファイルを別のシステムに読み込む前に、このパスワードを設定してください。このパスワードは、データベースに格納されている既存のパスワードよりも優先されます。パスワードが null の場合は、既存の null 以外のパスワード値が優先されます。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 現在の設定をファイルに書き出すには、「書き出し」をクリックして設定ファイルを別の場所に保存します。
1. In the file, locate the `Domains` > *[Your domain name]* > `DirectoryConfigs` > `LDAPGroupConfig` node. 以下に例を示します。

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

   `bindpassword` の値部分に値を入力して変更を保存します。

1. In the file, locate the `Domains` > *[Your domain name]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` node. 以下に例を示します。

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

   `bindpassword` の値部分に値を入力して変更を保存します。

1. 更新したファイルを読み込むには、User Management で、設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックしてファイルを探し、「読み込み」をクリックして「OK」をクリックします。

