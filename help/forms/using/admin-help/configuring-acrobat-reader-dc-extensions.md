---
title: データキャプチャのための Acrobat Reader DC Extensions の設定
description: データキャプチャのための Acrobat Reader DC Extensions の設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 100%

---

# データキャプチャのための Acrobat Reader DC Extensions の設定 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

AEM Forms インストール環境のユーザーが Content Services（非推奨）のデータキャプチャ機能を使用する場合、このユーザー用に、読み取り専用アクセス権を持つ役割を作成することをお勧めします。

***メモ&#x200B;**：Adobe® LiveCycle® Content Services ES（非推奨）は LiveCycle と共にインストールされるコンテンツ管理システムです。このサービスでは、人間中心のプロセスをデザイン、管理、監視および最適化することができます。Content Services（非推奨）のサポートは 2014年12月31日（PT）をもって終了しています。[アドビ製品のライフサイクルに関するドキュメント](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)を参照してください。*

データをキャプチャするには、SampleReaderExtensionsCredential にアクセスするために、ユーザーに役割を割り当てる必要があります。標準のトラスト管理者の役割を割り当てることができます。ただし、この役割を割り当てると、PKI 信頼設定を制御し PKI 認証情報を管理する管理者権限を管理者以外の一般ユーザーに与えることになるため、実稼働環境での AEM Forms インストールのセキュリティが危険にさらされる可能性があることを考慮してください。AEM Forms システム管理者が Trust Store への読み取り専用アクセス権のみを含む役割を作成して、データキャプチャ機能を使用する管理者以外のユーザーにこの役割を割り当てることをお勧めします。

## データキャプチャを行うユーザーの役割を作成 {#create-a-role-for-data-capture-users}

1. 管理コンソールで、設定／User Management／役割の管理をクリックし、「新しい役割」をクリックします。
1. 役割名（「データキャプチャユーザー」など）や説明を該当するフィールドに入力して、「次へ」をクリックします。
1. 役割の権限の画面で「権限を検索」をクリックし、使用可能な権限のリストから「資格情報読み取り」を選択します。
1. 「OK」、「完了」の順にクリックします。

## データキャプチャの役割を割り当て {#assign-the-data-capture-role}

1. 管理コンソールで、設定／User Management／役割の管理をクリックし、「検索」をクリックします。
1. 作成したデータキャプチャユーザーの役割をクリックします。
1. 「ユーザー／グループの役割」タブで、「ユーザーまたはグループを検索」をクリックします。
1. ユーザーおよびグループを検索画面で「検索」をクリックし、データキャプチャユーザーの役割を必要とするユーザーを選択して、「OK」をクリックします。
1. 役割を編集画面で、「保存」をクリックします。
