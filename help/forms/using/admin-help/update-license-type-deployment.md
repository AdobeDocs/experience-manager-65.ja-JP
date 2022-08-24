---
title: デプロイメントのライセンスの種類の更新
seo-title: Update the license type for the deployment
description: 管理コンソールのライセンスを変更ページを使用して、デプロイメントのライセンスの種類を更新します。
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 100%

---

# デプロイメントのライセンスの種類の更新 {#update-the-license-type-for-the-deployment}

AEM Forms インストールプロセスの一環として、Configuration Manager を使用し、必要な AEM Forms モジュールの設定とデプロイを行いました。デフォルトでは、これらのモジュールに 60 日間の評価版ライセンスが設定されています。デプロイメントのライセンスの種類を変更するには、管理コンソールのライセンスを変更ページを使用します。現在デプロイされているモジュールは、ライセンスを変更ページに表示されます。

ライセンスを変更ページにはライセンスに関する次の情報が表示されます。

* 現在のライセンスの種類
* ライセンスの最終更新日時
* 最終更新を実行したユーザー 
* ライセンスの現在のステータス 
* AEM Forms をインストールした日付
* 現在のライセンスが期限切れになる日付

>[!NOTE]
>
>ライセンスの変更はすべてのデプロイ済みモジュールに適用されます。ライセンスの種類を変更する前に、ライセンスを発行しないモジュールのデプロイを解除します。デプロイされているモジュールの一覧にアドビから購入したもの以外のモジュールが含まれている場合は、ライセンスの種類で「製品」を選択しないでください。

## ライセンスの種類の更新 {#update-the-license-type}

1. 管理コンソールで「ライセンス」をクリックします。
1. AEM Forms のエンドユーザー使用許諾契約書を読み、契約書の条項に同意する場合は「同意します」を選択し、「次へ」をクリックします。
1. ライセンスを変更ページでライセンスの種類を選択します。

   * **EVAL：** 60 日間の評価版ライセンス
   * **DEV：**&#x200B;無期限の開発ライセンス
   * **NFR：** 2 年間の評価版ライセンス
   * **IDEV：**&#x200B;アドビデベロッパープログラムの 1 年間の購読
   * **実稼働：**&#x200B;無期限のライセンス

1. 「はい、ライセンスの変更はデプロイ済みのすべてのモジュールに対して有効です」を選択します。
1. 「ライセンスの変更を確認」をクリックします。ライセンスが正常に更新されたことを示すメッセージが表示されます。
