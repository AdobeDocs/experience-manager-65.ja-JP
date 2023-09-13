---
title: データキャプチャ用のAcrobat Reader DC Extensions の設定
description: データキャプチャ用にAcrobat Reader DC Extensions を設定する方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 3%

---

# データキャプチャ用のAcrobat Reader DC Extensions の設定 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

AEM forms インストール環境のユーザーが Content Services（非推奨）のデータ取得機能を使用している場合、これらのユーザーに対して読み取り専用アクセス権を持つロールを作成することをお勧めします。

***注意&#x200B;**:Adobe®LiveCycle® Content Services ES（非推奨）は、LiveCycleと共にインストールされるコンテンツ管理システムです。 これにより、ユーザーは人間中心のプロセスを設計、管理、監視、最適化できます。 Content Services（非推奨）のサポートは12/31/2014で終了します。 [アドビ製品のライフサイクルに関するドキュメント](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)を参照してください。*

データ取得を行うには、SampleReaderExtensionsCredential にアクセスするためのユーザーロールを割り当てる必要があります。 標準の信頼管理者の役割を割り当てることができます。 ただし、この役割には、PKI の信頼設定を制御し、PKI 資格情報を管理する一般的な非管理者ユーザー管理者権限が与えられ、実稼動環境でのAEM forms のインストールのセキュリティが損なわれる可能性があると考えてください。 AEM forms システム管理者は、Trust Store への読み取り専用アクセス権のみを付与するロールを作成し、この新しいロールを、データ取得を使用する管理者以外のユーザーに割り当てることをお勧めします。

## データ取得ユーザーのロールの作成 {#create-a-role-for-data-capture-users}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「新しい役割」をクリックします。
1. ロール名（例：データ取得ユーザ）と説明を適切なフィールドに入力し、「次へ」をクリックします。
1. 役割の権限画面で、「権限を検索」をクリックし、使用可能な権限のリストから「Credential Read」を選択します。
1. 「OK」をクリックし、「完了」をクリックします。

## データキャプチャの役割を割り当てる {#assign-the-data-capture-role}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「検索」をクリックします。
1. 作成したデータ取得ユーザーの役割をクリックします。
1. [ 役割のユーザー/グループ ] タブで、[ ユーザー/グループの検索 ] をクリックします。
1. 「ユーザーおよびグループの検索」画面で「検索」をクリックし、データ取得ユーザーの役割を必要とするユーザーを選択して、「OK」をクリックします。
1. 役割を編集画面で、「保存」をクリックします。
