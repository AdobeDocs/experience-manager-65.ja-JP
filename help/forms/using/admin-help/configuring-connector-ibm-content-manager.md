---
title: IBM&reg; Content Manager 用の Connector の設定
description: Connector for IBM&reg; Content Manager を設定して、AEM forms とIBM&reg; Content Manager 間の通信を有効にします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---

# IBM® Content Manager 用の Connector の設定{#configuring-connector-for-ibm-content-manager}

IBM® Content Manager 用コネクタを使用すると、AEM forms とIBM® Content Manager 間の通信が可能になります。 その他の背景情報については、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## IBM® Content Manager 接続の設定 {#configure-the-ibm-content-manager-connection}

1. 管理コンソールで、サービス/IBM® Content Manager 用コネクタをクリックします。
1. 「データストア名」ボックスに、接続先のIBM® Content Manager データストアの名前を入力します。 データベースがローカルの場合は、データベースの名前を入力します。 データベースがリモートの場合は、そのエイリアス名を入力します。
1. 「 User Name 」ボックスに、IBM® Content Manager データストアに接続するユーザーのユーザー ID を入力します。
1. 「パスワード」ボックスに、ユーザーのパスワードを入力します。
1. （オプション）「Alias Connection String」ボックスに、追加の接続引数を入力します。 通常、このボックスは空にする必要があります。 詳しくは、 IBM®のドキュメントを参照してください。
1. 「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

誤った dataStore のエイリアス、ユーザー名、パスワードを入力した場合は、IBM® Content Manager サービス用の Content Repository Connector が実行されているかどうかに応じて、次の結果が返されます。

* サービスが停止している場合は、サービス構成情報を保存したときに、エラーは表示されません。 ただし、次回サービスを開始すると、例外がスローされ、サービスは開始されません。
* サービスが起動した場合、サービス構成情報を保存すると、サービスは資格情報の検証を直ちに試みます。 この場合、エラーが発生し、設定情報は保存されません。
