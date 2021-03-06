---
title: フォームと関連リソースの削除
seo-title: Deleting forms and related resources
description: AEM Forms でのフォームまたはアセットの削除方法と、参照先および参照元アセットと XFA フォームに対する影響。
seo-description: How to delete a form or an asset in AEM Forms and the impact on referenced and referring assets and XFA forms.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 100%

---

# フォームと関連リソースの削除 {#deleting-forms-and-related-resources}

フォームとアセットを削除して、これらのアセットをリポジトリから削除できます。削除操作は、すべてのアセットタイプとフォルダーに対して動作します。

オーサーインスタンスからアセットを削除すると、そのアセットはパブリッシュインスタンスからも削除されます。AEM Forms サーバーはオーサーインスタンスとパブリッシュインスタンスからなります。オーサーインスタンスは、フォームのアセットとリソースを作成したり管理したりするためのものです。パブリッシュインスタンスは、発行済みフォームのアセットと関連リソースを含み、これらはエンドユーザーが使用できます。

## フォームの削除方法 {#how-to-delete-a-form}

1. `https://[hostname]:'port'/aem/forms.html.` にアクセスして AEM Forms ユーザーインターフェイスにログインします。
1. 削除するフォームを探して移動します。ツールバーで ![aem6forms_delete2](assets/aem6forms_delete2.png) 削除をクリックし、削除操作を確定します。

   >[!NOTE]
   >
   >一度の 1 つのフォームのみ削除できます。複数のフォームの削除は、個別に行うかあるいは親フォルダーを削除します。

1. アセットを削除する前に、AEM Forms は参照をチェックし、明示的な確認を求めます。関係ステータスに無関係にアセットを削除する場合は、「削除を強制」をクリックします。

   >[!NOTE]
   >
   >他のアセットによって参照されているアセットを削除すると、機能に問題を起こす可能性があります。

   >[!NOTE]
   >
   >選択したアセットがフォルダーで、その階層にそのようなアセットが含まれている場合は、他のアセットを個別に削除するかあるいはフォルダー全体を削除します。

## 参照先 XFA フォームを削除した場合の影響 {#impact-of-deleting-a-referenced-xfa-form}

AEM Forms では、XFA フォームテンプレートは、アダプティブフォームまたは別の XFA フォームテンプレートによって参照されることができます。また、テンプレートはリソースまたは別の XFA テンプレートを参照することもできます。

アダプティブフォームによって参照されている XFA フォームを削除すると、アダプティブフォームを破損する可能性があるのでお勧めできません。アダプティブフォームが XFA フォームを参照しているときは、それらのフィールドは連結されています。XFA の削除後に、アダプティブフォームはそのフィールドを XFA のフィールドと同期できず、これらのフィールドに対してエラーメッセージを表示します。参照先 XFA の削除の影響と dirty アダプティブフォームの詳細については、[参照先 XFA フォームの更新](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)を参照してください。

このような XFA フォームを削除するには、アダプティブフォームを更新し、XFA フィールドとの連結を削除します。
