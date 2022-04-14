---
title: タスクマネージャーエンドポイントの設定
seo-title: Configuring Task Manager endpoints
description: タスクマネージャーエンドポイントを設定する方法について説明します。
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '232'
ht-degree: 100%

---

# タスクマネージャーエンドポイントの設定 {#configuring-task-manager-endpoints}

タスクマネージャーエンドポイントを使用すると、Workspace ユーザーがサービスを呼び出せるようになります。

**タスクマネージャーエンドポイントの設定**

タスクマネージャーエンドポイントを設定するには、次の設定を使用します。

**名前：**（必須）エンドポイントを識別します。名前は Workspace のカードビューで表示されます。&lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：**&#x200B;エンドポイントの説明。&lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**タスクの手順：**&#x200B;このワークフローを開始するユーザーに対する指示です。

**プロセスの所有者：**&#x200B;プロセスを所有する個人の名前です。

**ユーザーはタスクの転送が可能：**&#x200B;初期タスクの転送をユーザーに許可します。

**添付ファイルウィンドウを表示：**&#x200B;添付ファイルウィンドウの表示をユーザーに許可します。

**添付ファイルの追加を許可：**&#x200B;添付ファイルとメモの追加をユーザーに許可します。

**初期タスクをロック：**&#x200B;初期タスクをロックします。

**共有キュー用の ACL を追加：**&#x200B;共有キューユーザー用の ACL で初期タスクを作成します。

**分類：**（必須）Workspace でフォームが表示されるカテゴリです。リストからカテゴリを選択するか、「新規カテゴリ」を選択して、カテゴリを追加します。

**操作名：**（必須）エンドポイントに割り当てることができる操作のリストです。
