---
title: デプロイメントのライセンスの種類の更新
description: 管理コンソールのライセンスを変更ページを使用して、デプロイメントのライセンスの種類を更新します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '270'
ht-degree: 100%

---

# デプロイメントのライセンスの種類の更新 {#update-the-license-type-for-the-deployment}

AEM Forms インストールプロセスの一環として、Configuration Manager を使用し、必要な AEM Forms モジュールの設定とデプロイを行いました。デフォルトでは、これらのモジュールに 60 日間の評価版ライセンスが設定されています。デプロイメントのライセンスタイプを変更するには、管理コンソールのライセンスを変更ページを使用します。現在デプロイされているモジュールは、ライセンスを変更ページに表示されます。

ライセンスを変更ページには、ライセンスに関する次の情報が表示されます。

* 現在のライセンスタイプ
* ライセンスの最終更新日時
* 最終更新を実行したユーザー
* ライセンスの現在のステータス
* AEM Forms をインストールした日付
* 現在のライセンスが期限切れになる日付

>[!NOTE]
>
>ライセンスの変更は、すべてのデプロイ済みモジュールに適用されます。ライセンスタイプを変更する前に、ライセンスを発行しないモジュールのデプロイを解除します。デプロイ済みモジュールの一覧にアドビから購入したもの以外のモジュールが含まれている場合は、ライセンスタイプに「実稼動」を選択しないでください。

## ライセンスタイプの更新 {#update-the-license-type}

1. 管理コンソールで、「ライセンス」をクリックします。
1. AEM Forms のエンドユーザー使用許諾契約を読み、契約の条項に同意する場合は「同意します」を選択し、「次へ」をクリックします。
1. ライセンスを変更ページで、ライセンスタイプを選択します。

   * **EVAL：** 60 日間の評価版ライセンス
   * **DEV：**&#x200B;無期限の開発ライセンス
   * **NFR：** 2 年間の評価版ライセンス
   * **IDEV：** Adobe Developer プログラムの 1 年間の購読
   * **実稼働：**&#x200B;無期限のライセンス

1. 「はい、ライセンスの変更はデプロイ済みのすべてのモジュールに対して有効です」を選択します。
1. 「ライセンスの変更を確認」をクリックします。ライセンスが正常に更新されたことを示すメッセージが表示されます。
