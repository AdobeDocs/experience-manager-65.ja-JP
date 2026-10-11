---
title: IBM&reg; Content Manager用コネクタの設定
description: IBM&reg; Content Manager用コネクタを設定して、AEM フォームとIBM&reg; Content Manager間のコミュニケーションを有効にします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
source-wordcount: '288'
ht-degree: 90%
---
# IBM® Content Manager 用コネクターの設定{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

IBM® Content Manager 用コネクターを使用すると、AEM Forms とIBM® Content Manager 間の通信が可能になります。 その他の背景情報について詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)にある「ECM 用コネクター」を参照してください。

## IBM® Content Manager 接続を設定 {#configure-the-ibm-content-manager-connection}

1. 管理コンソールで、サービス／IBM® Content Manager 用コネクターの順にクリックします。
1. 「データストア名」ボックスに、接続先の IBM® Content Manager データストアの名前を入力します。 データベースがローカルの場合は、データベースの名前を入力します。 データベースがリモートの場合は、データベースのエイリアス名を入力します。
1. 「ユーザー名」ボックスに、IBM® Content Manager データストアに接続するユーザーのユーザー ID を入力します。
1. 「パスワード」ボックスに、ユーザーのパスワードを入力します。
1. （オプション）「エイリアス接続文字列」ボックスに、追加の接続引数を入力します。 通常、このボックスは空にしておく必要があります。 詳しくは、IBM® のドキュメントを参照してください。
1. 「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

誤ったデータストアのエイリアス、ユーザー名やパスワードを入力すると、IBM® Content Manager サービス用コンテンツリポジトリコネクターが実行中かどうかに応じて、次の結果になります。

* サービスが停止している場合、サービス設定情報を保存したときに、エラーは表示されません。 ただし、次回サービスを起動すると、例外が発生し、サービスは起動しません。
* サービス設定情報を保存したときにサービスが起動している場合、サービスは資格情報をすぐに検証しようとします。 この場合はエラーが発生し、設定情報は保存されません。
