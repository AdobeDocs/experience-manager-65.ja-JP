---
title: データキャプチャのための Acrobat Reader DC Extensions の設定
description: データキャプチャのための Acrobat Reader DC Extensions の設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%
---
# データキャプチャのための Acrobat Reader DC Extensions の設定 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

AEM Forms インストール環境のユーザーが Content Services（非推奨）のデータキャプチャ機能を使用する場合、このユーザー用に、読み取り専用アクセス権を持つ役割を作成することをお勧めします。

***メモ&#x200B;**：Adobe® LiveCycle® Content Services ES（非推奨）は LiveCycle と共にインストールされるコンテンツ管理システムです。 このサービスでは、人間中心のプロセスをデザイン、管理、監視および最適化することができます。 Content Services（非推奨）のサポートは 2014年12月31日（PT）をもって終了しています。 [アドビ製品のライフサイクルに関するドキュメント](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)を参照してください。*

データをキャプチャするには、SampleReaderExtensionsCredential にアクセスするために、ユーザーに役割を割り当てる必要があります。 標準のトラスト管理者の役割を割り当てることができます。 ただし、この役割を割り当てると、PKI 信頼設定を制御し PKI 認証情報をコントロールする管理者権限を、管理者以外の一般ユーザーに与えることになるため、本番環境での AEM Forms インストールのセキュリティが危険にさらされる可能性があることを考慮してください。 AEM Forms システム管理者が Trust Store への読み取り専用アクセス権のみを含む役割を作成して、データキャプチャ機能を使用する管理者以外のユーザーに、この役割を割り当てることをお勧めします。

## データキャプチャを行うユーザーの役割を作成 {#create-a-role-for-data-capture-users}

1. 管理コンソールで、設定／ユーザー管理／役割の管理をクリックし、「新しい役割」をクリックします。
1. 役割名（「データキャプチャユーザー」など）や説明を該当するフィールドに入力して、「次へ」をクリックします。
1. 役割の権限の画面で「権限を検索」をクリックし、使用可能な権限のリストから「資格情報読み取り」を選択します。
1. 「OK」、「完了」の順にクリックします。

## データキャプチャの役割を割り当て {#assign-the-data-capture-role}

1. 管理コンソールで、設定／ユーザー管理／役割の管理をクリックし、「検索」をクリックします。
1. 作成したデータキャプチャユーザーの役割をクリックします。
1. 「ユーザー／グループの役割」タブで、「ユーザーまたはグループを検索」をクリックします。
1. ユーザーおよびグループを検索画面で「検索」をクリックし、データキャプチャユーザーの役割を必要とするユーザーを選択して、「OK」をクリックします。
1. 「役割を編集」画面で、「保存」をクリックします。
