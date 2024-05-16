---
title: IBM&reg; Content Manager 用コネクターの設定
description: IBM&reg; Content Manager 用コネクターを設定して、AEM Forms と IBM&reg; Content Manager 間の通信を有効にします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '273'
ht-degree: 100%

---

# IBM Content Manager 用コネクターの設定{#configuring-connector-for-ibm-content-manager}

IBM® Content Manager 用コネクターを使用すると、AEM Forms とIBM® Content Manager 間の通信が可能になります。その他の背景情報について詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)にある「ECM 用コネクター」を参照してください。

## IBM® Content Manager 接続を設定 {#configure-the-ibm-content-manager-connection}

1. 管理コンソールで、サービス／IBM® Content Manager 用コネクターの順にクリックします。
1. 「データストア名」ボックスに、接続先の IBM® Content Manager データストアの名前を入力します。データベースがローカルの場合は、データベースの名前を入力します。データベースがリモートの場合は、データベースのエイリアス名を入力します。
1. 「ユーザー名」ボックスに、IBM® Content Manager データストアに接続するユーザーのユーザー ID を入力します。
1. 「パスワード」ボックスに、ユーザーのパスワードを入力します。
1. （オプション）「エイリアス接続文字列」ボックスに、追加接続の引数を入力します。通常、このボックスは空にしておく必要があります。詳しくは、IBM® のドキュメントを参照してください。
1. 「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

誤ったデータストアのエイリアス、ユーザー名やパスワードを入力すると、IBM® Content Manager サービス用コンテンツリポジトリコネクターが実行中かどうかに応じて、次の結果になります。

* サービスが停止している場合、サービス設定情報を保存したときに、エラーは表示されません。ただし、次回サービスを起動すると、例外が発生し、サービスは起動しません。
* サービス設定情報を保存したときにサービスが起動している場合、サービスは資格情報をすぐに検証しようとします。この場合はエラーが発生し、設定情報は保存されません。
