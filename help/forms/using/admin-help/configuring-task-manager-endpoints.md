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
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 51%

---

# タスクマネージャーエンドポイントの設定 {#configuring-task-manager-endpoints}

タスクマネージャーエンドポイントを使用すると、Workspace ユーザーがサービスを呼び出せるようになります。

**タスクマネージャーエンドポイントの設定**

タスクマネージャーエンドポイントを設定するには、次の設定を使用します。

**名前：** （必須）エンドポイントを識別します。名前は Workspace のカード表示で表示されます。&lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：** エンドポイントの説明。&lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**タスクの手順：** このワークフローを開始するユーザーに対する手順。

**プロセスの所有者：** プロセスを担当する個人の名前。

**User Can Forward Task:** ユーザーが最初のタスクを転送できるようにします。

**添付ファイルウィンドウを表示：** ユーザーが添付ファイルウィンドウを表示できるようにします。

**添付ファイルの追加を許可：** ユーザーが添付ファイルとメモを追加できるようにします。

**Task Initially Locked:** 初期タスクをロックします。

**共有キューのACLを追加：** 共有キューユーザーのACLを使用して初期タスクが作成されます。

**分類：** （必須）ユーザーがWorkspaceでフォームを表示するカテゴリ。リストからカテゴリを選択するか、「新規カテゴリ」を選択して、カテゴリを追加します。

**操作名：** （必須）エンドポイントに割り当てることができる操作のリスト。
