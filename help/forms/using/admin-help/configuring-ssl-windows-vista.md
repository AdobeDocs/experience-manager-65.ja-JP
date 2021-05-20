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
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 64%

---

# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

Windows Vista™ で SSL を設定するには、認証時に RSA 鍵が設定された SSL 秘密鍵証明書が必要になります。Java keytool を使用して、証明書を作成できます。

>[!NOTE]
>
>Windows Vista は DSA 鍵には対応していません。

証明書およびキーストアの作成に必要なすべての情報を指定した 1 つのコマンドを使用することにより、keytool を実行できます。

**SSL 証明書の作成**

1. コマンドプロンプトで&#x200B;*`[JAVA HOME]`*/binに移動し、次のコマンドを入力して証明書とキーストアを作成します。

   `keytool -genkey -keyalg RSA -dname "CN=`*ホス* `, OU=`*ト名* `, O=`*グル* `,L=`*ープ名会社名* `, S=`** `, C=`*前都市名状態国コード* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* ** `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`をJDKがインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。*

1. パスワードとして`changeit`と入力します。 Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
