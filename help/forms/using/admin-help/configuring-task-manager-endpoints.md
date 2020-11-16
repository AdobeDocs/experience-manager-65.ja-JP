---
title: タスクマネージャーエンドポイントの設定
seo-title: タスクマネージャーエンドポイントの設定
description: タスクマネージャーエンドポイントを設定する方法について説明します。
seo-description: タスクマネージャーエンドポイントを設定する方法について説明します。
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 51%

---


# タスクマネージャーエンドポイントの設定 {#configuring-task-manager-endpoints}

タスクマネージャーエンドポイントを使用すると、Workspace ユーザーがサービスを呼び出せるようになります。

**タスクマネージャーエンドポイントの設定**

タスクマネージャーエンドポイントを設定するには、次の設定を使用します。

**名前：** （必須）エンドポイントを識別します。 名前は Workspace のカード表示で表示されます。&lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：** エンドポイントの説明です。 &lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**タスク手順：** このワークフローを開始するユーザーに対する手順です。

**プロセスの所有者：** プロセスの責任者の名前。

**User Can Forwardタスク:** 最初のタスクを転送できます。

**添付ファイルウィンドウを表示：** 添付ファイルウィンドウの表示をユーザーに許可します。

**添付ファイルの追加を許可：** 添付ファイルとメモの追加をユーザーに許可します。

**タスクの初期ロック：** 初期タスクをロックします。

**Shared Queues追加のACL:** 共有キューユーザーのACLを使用して初期タスクが作成されます。

**分類：** （必須）Workspaceでフォームを表示するカテゴリです。 リストからカテゴリを選択するか、「新規カテゴリ」を選択して、カテゴリを追加します。

**操作名：** （必須）エンドポイントに割り当てることができる操作のリスト。
