---
title: タスクマネージャーエンドポイントの設定
description: サービスを呼び出せるようにタスクマネージャーエンドポイントを設定する方法について説明します。 タスクマネージャーエンドポイントを設定するには、様々な設定が必要です。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
source-wordcount: '245'
ht-degree: 100%
---
# タスクマネージャーエンドポイントの設定 {#configuring-task-manager-endpoints}

タスクマネージャーエンドポイントを使用すると、Workspace ユーザーがサービスを呼び出せるようになります。

**タスクマネージャーエンドポイントの設定**

タスクマネージャーエンドポイントを設定するには、次の設定を使用します。

**名前：**（必須）エンドポイントを識別します。 名前は Workspace のカードビューで表示されます。 &lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。 エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：**&#x200B;エンドポイントの説明。 &lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**タスクの手順：**&#x200B;このワークフローを開始するユーザーに対する指示です。

**プロセスの所有者：**&#x200B;プロセスを所有する個人の名前です。

**ユーザーはタスクの転送が可能：**&#x200B;初期タスクの転送をユーザーに許可します。

**添付ファイルウィンドウを表示：**&#x200B;添付ファイルウィンドウの表示をユーザーに許可します。

**添付ファイルの追加を許可：**&#x200B;添付ファイルとメモの追加をユーザーに許可します。

**初期タスクをロック：**&#x200B;初期タスクをロックします。

**共有キュー用の ACL を追加：**&#x200B;共有キューユーザー用の ACL で初期タスクを作成します。

**分類：**（必須）Workspace でフォームが表示されるカテゴリです。 リストからカテゴリを選択するか、「新規カテゴリ」を選択して、カテゴリを追加します。

**操作名：**（必須）エンドポイントに割り当てることができる操作のリストです。
