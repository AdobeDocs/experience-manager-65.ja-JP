---
title: Windows Vista での SSL の設定
description: Windows Vista で SSL を設定する方法を説明します。 を使用して Java Keytool を実行し、認証用の RSA キーを含む SSL 証明書を生成します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 50%

---

# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

Windows Vista™で SSL を設定するには、認証用に RSA キーを持つ SSL 証明書が必要です。 Java keytool を使用して証明書を作成できます。

>[!NOTE]
>
>Windows Vista は、DSA キーでは機能しません。

証明書とキーストアの作成に必要なすべての情報を含む 1 つのコマンドを使用して、keytool を実行できます。

**SSL 証明書の作成**

1. コマンドプロンプトで、*`[JAVA HOME]`*/bin に移動し、以下のコマンドを入力して証明書とキーストアを作成します。

   `keytool -genkey -keyalg RSA -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `,L=`*市区町村名* `, S=`*都道府県* `, C=`*国コード* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *パスワード* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`は JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。*

1. パスワードに `changeit` と入力します。Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
