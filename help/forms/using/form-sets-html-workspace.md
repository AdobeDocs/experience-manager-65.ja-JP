---
title: AEM Forms Workspace のフォームセットの使用
description: フォームセットは、HTML5 のフォームの集まりで、エンドユーザーには 1 つのフォームのセットとして表示されます。 AEM Forms Workspace でフォームセットを使用する方法を説明します。
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 60%

---

# AEM Forms Workspace のフォームセットの使用{#working-with-formsets-in-aem-forms-workspace}

フォームセットは、HTML5 のフォームの集まりで、エンドユーザーには 1 つのフォームのセットとして表示されます。 エンドユーザーがフォームセットの入力を開始すると、フォームが別のフォームにシームレスに切り替わります。 その後、フォームのセットを 1 回のクリックで送信できます。 フォームセットおよびその設定方法について詳しくは、[AEM Forms のフォームセット](../../forms/using/formset-in-aem-forms.md)を参照してください。

AEM Forms workspace はフォームセットをサポートしています。 フォームセットを使用すると、1 つのサービスまたはプロセスに関連する複数のフォームをグループ化して、ビジネスプロセスを自動化し、エンドユーザーに表示できます。 このシナリオでは、ユーザーはセット全体を 1 つとして入力でき、個々のフォームやプロセスをファイル化、送信、追跡する必要はありません。

## AEM Forms Workspace アプリケーションにおけるフォームセットのスタートポイントへの割り当て {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Workbench でビジネスプロセスのワークフローを作成します。詳しくは、[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。
1. スタートポイントの「Process Properties」の「Presentation &amp; Data」で、「**CRX アセットを使用する**」を選択します。

   ![1-3](assets/1-3.png)

1. CRX アセットパスの横にある「![参照](assets/browse.png)」（参照）をクリックします。フォームアセットを選択ダイアログが表示されます。

   ![2-1](assets/2-1.png)

1. 「**フォームセット**」タブをクリックし、関連するフォームセットをリストから選択して、「**OK**」をクリックします。

1. 他の関連プロセスのプロパティを更新したら、アプリケーションをデプロイします。

## AEM Forms Workspace でのフォームセットの使用 {#using-formset-in-nbsp-aem-forms-workspace}

フォームセットをスタートポイントに割り当てると、このスタートポイントを、他のすべてのスタートポイントと同様に、AEM Forms Workspace から呼び出せるようになります。

AEM Forms Workspace を通じてフォームセットでサポートされる操作は次のとおりです。

* ドラフトとして保存
* ロック
* 中断
* 送信
* 添付ファイルを追加
* メモを追加
* 「戻る」または「次へ」ボタンを使用してフォームセット内のフォーム間を移動する

![3-1](assets/3-1.png)

>[!NOTE]
>
>フォームセット内で前のフォームや次のフォームに移動する際のパフォーマンスを向上するため、Workspace のすべてのボタン（「戻る」、「次へ」、「保存」、「送信」など）は、関連フォームのレンダリングが終了するまで無効になります。
