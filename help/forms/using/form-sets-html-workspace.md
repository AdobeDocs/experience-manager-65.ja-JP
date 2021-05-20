---
title: AEM Forms Workspace のフォームセットの使用
seo-title: AEM Forms Workspace のフォームセットの使用
description: フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。AEM Forms Workspace でフォームセットを使用する方法について説明します。
seo-description: フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。AEM Forms Workspace でフォームセットを使用する方法について説明します。
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 73%

---

# AEM Forms Workspace のフォームセットの使用{#working-with-formsets-in-aem-forms-workspace}

フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。エンドユーザーがフォームセットへの入力を始めると、フォームセットはその内容を別のフォームにもシームレスに移行します。フォームセットは 1 回クリックすれば送信できます。フォームセットとその設定方法について詳しくは、「AEM Formsの[フォームセット](../../forms/using/formset-in-aem-forms.md)」を参照してください。

AEM Forms Workspace はフォームセットをサポートします。フォームセットでは、サービスやプロセスに関連する複数のフォームをグループ化し、ビジネス上のプロセスを自動化するとともにエンドユーザーに表示します。このようなシナリオでは、ユーザーはセット全体を 1 つとして記入し、個々のフォームやプロセスをファイル、送信、追跡する必要はありません。

## AEM Forms Workspace アプリケーションにおけるフォームセットのスタートポイントへの割り当て {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Workbench でビジネスプロセスのワークフローを作成します。詳しくは、[Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。
1. スタートポイントのプロセスプロパティから、「Presentation &amp; Data」で「**Use A CRX Asset**」を選択します。

   ![1-3](assets/1-3.png)

1. CRXアセットパスの横にある![browse](assets/browse.png)(Browse)をクリックします。 フォームアセットを選択ダイアログが表示されます。

   ![2-1](assets/2-1.png)

1. 「**フォームセット**」タブをクリックし、リストから目的のフォームセットを選択して、「**OK**」をクリックします。

1. 他の関連するプロセスプロパティを更新した後に、アプリケーションをデプロイします。

## AEM Forms Workspace でのフォームセットの使用 {#using-formset-in-nbsp-aem-forms-workspace}

フォームセットをスタートポイントに関連付けると、他のスタートポイントが呼び出されると同時に、AEM Forms Workspaceからスタートポイントを呼び出すことができます。

AEM Forms Workspace を通じてフォームセットでサポートされる操作は次のとおりです。

* ドラフトとして保存
* Lock
* 中断
* 送信
* 添付ファイルを追加
* メモを追加
* 「戻る」または「次へ」ボタンを使用したフォームセット内の移動

![3-1](assets/3-1.png)

>[!NOTE]
>
>フォームセット内で前のフォームや次のフォームに移動する際のパフォーマンスを向上するため、Workspace のすべてのボタン（「戻る」、「次へ」、「保存」、「送信」、「...」（詳細））は、関連フォームのレンダリングが終了するまで無効になります。
