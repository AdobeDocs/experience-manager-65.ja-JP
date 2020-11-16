---
title: Connector for IBM Content Manager の設定
seo-title: Connector for IBM Content Manager の設定
description: Connector for IBM Content Manager を、AEM Forms と IBM Content Manager 間の通信を可能にするように設定します。
seo-description: Connector for IBM Content Manager を、AEM Forms と IBM Content Manager 間の通信を可能にするように設定します。
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 98%

---


# Connector for IBM Content Manager の設定{#configuring-connector-for-ibm-content-manager}

Connector for IBM Content Manager は、AEM Forms と IBM Content Manager 間の通信を可能にします。関連する参考情報については、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」の「Connectors for ECM」を参照してください。

## IBM Content Manager 接続の設定 {#configure-the-ibm-content-manager-connection}

1. 管理コンソールで、サービス／Connector for IBM Content Manager をクリックします。
1. 「データストア名」ボックスに、接続先の IBM Content Manager データストアの名前を入力します。データベースがローカルの場合は、データベース名を入力します。データベースがリモートの場合は、データベースのエイリアス名を入力します。
1. 「ユーザー名」ボックスに、IBM Content Manager データストアに接続するユーザーのユーザー ID を入力します。
1. 「パスワード」ボックスに、ユーザーのパスワードを入力します。
1. （オプション）「接続文字列のエイリアス」ボックスで、追加接続の引数を入力します。ほとんどの場合、このボックスは空になっています。関連情報については、IBM のドキュメントを参照してください。
1. 「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

誤ったデータストアのエイリアス、ユーザー名またはパスワードを入力すると、Content Repository Connector for IBM Content Manager サービスが実行中かどうかに応じて、次の結果になります。

* サービス設定情報を保存したときにサービスが停止している場合、エラーは表示されません。ただし、次回サービスを起動すると、例外が発生し、サービスは起動しません。
* サービス設定情報を保存したときにサービスが起動している場合、サービスは秘密鍵証明書の情報をすぐに確認しようとします。この場合、エラーが発生し、設定情報は保存されません。

