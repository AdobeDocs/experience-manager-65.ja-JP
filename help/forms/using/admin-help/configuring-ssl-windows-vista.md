---
title: Windows Vista での SSL の設定
seo-title: Windows Vista での SSL の設定
description: Windows Vista での SSL の設定方法について説明します。
seo-description: Windows Vista での SSL の設定方法について説明します。
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

Windows Vista™ で SSL を設定するには、認証時に RSA 鍵が設定された SSL 秘密鍵証明書が必要になります。Java keytool を使用して、証明書を作成できます。

>[!NOTE]
>
>Windows Vista は DSA 鍵には対応していません。

証明書およびキーストアの作成に必要なすべての情報を指定した 1 つのコマンドを使用することにより、keytool を実行できます。

**SSL 証明書の作成**

1. In a command prompt, navigate to *`[JAVA HOME]`*/bin and type the following command to create the certificate and keystore:

   `keytool -genkey -keyalg RSA -dname "CN=`*Host Name Group Name *`, OU=`*Name*`, O=`*Name *Name Name Name Name Company`,L=`*State Country Country Country Country Code Cort Rename Password Name Password Key*`, S=`**`, C=`**`" -alias`**`-keypass``key`****`-keystore`**Group Group Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name Name No Name Name Name Name No Nout Co Co Cout Co Co Cout`.keystore`

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.*

1. Type `changeit` as the password. Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。

