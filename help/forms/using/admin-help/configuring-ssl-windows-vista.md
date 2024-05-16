---
title: Windows Vista での SSL の設定
description: Windows Vista での SSL の設定方法について説明します。Java keytool を使用して実行し、認証用の RSA 鍵を含む SSL 証明書を生成します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '173'
ht-degree: 100%

---

# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

Windows Vista™ で SSL を設定するには、認証用の RSA 鍵が設定された SSL 証明書が必要になります。Java keytool を使用して、証明書を作成できます。

>[!NOTE]
>
>Windows Vista は DSA 鍵には対応していません。

証明書とキーストアの作成に必要なすべての情報を含む 1 つのコマンドを使用して、keytool を実行できます。

**SSL 証明書の作成**

1. コマンドプロンプトで、*`[JAVA HOME]`*/bin に移動し、以下のコマンドを入力して証明書とキーストアを作成します。

   `keytool -genkey -keyalg RSA -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `,L=`*市区町村名* `, S=`*都道府県* `, C=`*国コード* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *パスワード* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`は JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。*

1. パスワードに `changeit` と入力します。Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
