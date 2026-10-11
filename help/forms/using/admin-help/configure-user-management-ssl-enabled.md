---
title: SSL 対応の LDAP サーバーを対象としたユーザー管理の設定
description: SSL 対応の LDAP サーバーを対象として User Management を設定し、LDAPS 経由で同期が正しく機能するようにする方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 94%
---
# SSL 対応の LDAP サーバーを対象としたユーザー管理の設定 {#configure-user-management-for-an-ssl-enabled-ldap-server}

同期が LDAPS を介して正しく動作するには、認証局（CA）によって発行された LDAP 証明書をアプリケーションサーバーの Java ランタイム環境（JRE）に配置する必要があります。 証明書をアプリケーションサーバーの JRE cacerts ファイルに読み込みます。通常、このファイルは *[JAVA_HOME]*/jre/lib/security/cacerts ディレクトリにあります。

1. ディレクトリサーバーで SSL を有効にします。 詳しくは、ディレクトリのベンダーによって提供されたマニュアルを参照してください。
1. ディレクトリサーバーからクライアント証明書を書き出します。
1. keytool プログラムを使用して、クライアント証明書ファイルを、AEM Forms アプリケーションサーバーのデフォルトの Java 仮想マシン（JVM™）証明書ストアに読み込みます。 このタスクの手順は、使用している JVM とクライアントのインストールパスによって異なります。 例えば、BEA WebLogic Server と JDK 1.5 を使用する場合、コマンドプロンプトで次のテキストを入力します。

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. プロンプトが表示されたら、パスワードを入力します （Javaの場合、デフォルトのパスワードは`changeit`です）。 証明書が正常に読み込まれたことを示すメッセージが表示されます。
1. プロンプトが表示されたら、`Yes` と入力して証明書を信頼します。
1. ユーザー管理で SSL を有効化し、ディレクトリの設定を行う場合は、「SSL」オプションで「はい」を選択して、ポート設定を変更します。 デフォルトのポート番号は 636 です。

>[!NOTE]
>
>SSL を使用する際に問題が発生した場合は、LDAP ブラウザーを使用して、SSL を使用しているときに LDAP システムにアクセスできるかどうかを確認します。 LDAP ブラウザーでアクセスできない場合は、証明書またはアプリケーションサーバーが正しく設定されていません。 LDAP ブラウザーが正常に動作していても引き続き問題が発生する場合は、ユーザー管理が正しく設定されていません。
