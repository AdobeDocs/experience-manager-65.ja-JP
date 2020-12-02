---
title: SSL 対応の LDAP サーバーを対象とした User Management の設定
seo-title: SSL 対応の LDAP サーバーを対象とした User Management の設定
description: SSL 対応の LDAP サーバーを対象として User Management を設定し、同期を有効にして LDAPS 経由で正しく動作させる方法について説明します。
seo-description: SSL 対応の LDAP サーバーを対象として User Management を設定し、同期を有効にして LDAPS 経由で正しく動作させる方法について説明します。
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 92%

---


# SSL 対応の LDAP サーバーを対象とした User Management の設定 {#configure-user-management-for-an-ssl-enabled-ldap-server}

同期が LDAPS を介して正しく動作するには、認証局（CA）によって発行された LDAP 証明書をアプリケーションサーバーの Java ランタイム環境（JRE）に配置する必要があります。証明書をアプリケーションサーバーのJRE cacertsファイルに読み込みます。通常、このファイルは&#x200B;*[JAVA_HOME]*/jre/lib/security/cacertsディレクトリにあります。

1. ディレクトリサーバーで SSL を有効にします。詳しくは、ディレクトリのベンダーによって提供されたマニュアルを参照してください。
1. ディレクトリサーバーからクライアント証明書を書き出します。
1. keytool プログラムを使用して、クライアント証明書ファイルを、AEM Forms アプリケーションサーバーのデフォルトの Java 仮想マシン（JVM™）証明書ストアに読み込みます。このタスクの手順は、使用している JVM とクライアントのインストールパスによって異なります。例えば、BEA WebLogic Server と JDK 1.5 を使用している場合は、コマンドプロンプトで次のテキストを入力します。

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. プロンプトが表示されたら、パスワードを入力します（Java では、デフォルトのパスワードは `changeit` です）。証明書が正常に読み込まれたことを示すメッセージが表示されます。
1. プロンプトが表示されたら、`Yes` と入力して証明書を信頼します。
1. User Management で SSL を有効化し、ディレクトリの設定を行う場合は、「SSL」オプションで「はい」を選択して、ポート設定を変更します。デフォルトのポート番号は 636 です。

>[!NOTE]
>
>SSL を使用する際に問題が発生した場合は、LDAP ブラウザーを使用して、SSL を使用しているときに LDAP システムにアクセスできるかどうかを確認してください。LDAP ブラウザーでアクセスできない場合は、証明書またはアプリケーションサーバーが正しく設定されていません。LDAP ブラウザーが正常に動作していても引き続き問題が発生する場合は、User Management が正しく設定されていません。

