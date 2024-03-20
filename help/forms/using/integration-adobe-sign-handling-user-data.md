---
title: Adobe Sign との統合| ユーザーデータの処理
description: アダプティブフォームで電子署名を行うための AEM Forms と Adobe Sign の統合について説明します。様々なワークフローに対して複数の署名オプションをサポートします。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 100%

---

# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] を と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。[!DNL  Adobe Sign]これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

1 人または複数の署名者がアダプティブフォームに署名をして送信するときに、署名者に関する情報を含む [!DNL Adobe Sign] の契約書が生成されます。

[!DNL AEM Forms] の [!DNL Adobe Sign] との統合について詳しくは、[アダプティブフォームで Adobe Sign を使用する](/help/forms/using/working-with-adobe-sign.md)を参照してください。

## ユーザーデータとデータストア {#data}

[!DNL Adobe Sign] 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。[!DNL Adobe Sign] サービスは、契約書内の署名を使用してユーザーデータを格納します。この契約書は、[!DNL AEM Forms] クラウドサービスに設定された [!DNL Adobe Sign] サーバーに保存されます。さらに、Forms ポータルの送信アクションを使用するようにアダプティブフォームが構成されている場合、契約書のデータはフォームデータと共に Forms ポータルのデータストアに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約書内で収集されますが、いずれのサービステーブルにも保存されません。[!DNL Adobe Sign] を使用すると、管理者はサービスで管理する管理データを自身で選択できます。[!DNL Adobe Sign] サービスのプライバシー管理者は、依頼者のメールアドレスに基づいて契約書のリストの作成または削除を行うことができます。

[!DNL Adobe Sign] は、参加者による契約書の検索、および必要に応じて契約書の削除を実行できる web アプリケーションを提供しています。詳しくは、[Adobe Sign - 機能：ユーザー情報の削除](https://helpx.adobe.com/jp/sign/help/adobesign_gdpr_user_deletion.html)を参照してください。

Forms ポータルの送信アクションを使用するように構成されているアダプティブフォームの契約書データも、Forms ポータルのデータストアに格納されます。Forms ポータルのデータストアにアクセスしてデータを削除する方法については、[Forms ポータル | ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md)を参照してください。
