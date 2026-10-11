---
title: Adobe Sign との統合| ユーザーデータの処理
description: アダプティブフォームで電子署名を行うための AEM Forms と Adobe Sign の統合について説明します。 様々なワークフローに対して複数の署名オプションをサポートします。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: a16aea24-4e85-528d-9377-cd80bb039c1d
    internal-label: Acrobat Sign
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%
---
# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] を [!DNL  Adobe Sign] と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。 これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

1 人または複数の署名者がアダプティブフォームに署名をして送信するときに、署名者に関する情報を含む [!DNL Adobe Sign] の契約書が生成されます。

[!DNL AEM Forms] の [!DNL Adobe Sign] との統合について詳しくは、[アダプティブフォームで Adobe Sign を使用する](/help/forms/using/working-with-adobe-sign.md)を参照してください。

## ユーザーデータとデータストア {#data}

[!DNL Adobe Sign] 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。 [!DNL Adobe Sign] サービスは、契約書内の署名を使用してユーザーデータを格納します。 この契約書は、[!DNL AEM Forms] クラウドサービスに設定された [!DNL Adobe Sign] サーバーに保存されます。 さらに、Forms ポータルの送信アクションを使用するようにアダプティブフォームが構成されている場合、契約書のデータはフォームデータと共に Forms ポータルのデータストアに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約書内で収集されますが、いずれのサービステーブルにも保存されません。 [!DNL Adobe Sign] を使用すると、管理者はサービスで管理する管理データを自身で選択できます。 [!DNL Adobe Sign] サービスのプライバシー管理者は、依頼者のメールアドレスに基づいて契約書のリストの作成または削除を行うことができます。

[!DNL Adobe Sign] は、参加者による契約書の検索、および必要に応じて契約書の削除を実行できる web アプリケーションを提供しています。 詳しくは、[Adobe Sign - 機能：ユーザー情報の削除](https://helpx.adobe.com/jp/sign/help/adobesign_gdpr_user_deletion.html)を参照してください。

Forms ポータルの送信アクションを使用するように構成されているアダプティブフォームの契約書データも、Forms ポータルのデータストアに格納されます。 Forms ポータルのデータストアにアクセスしてデータを削除する方法については、[Forms ポータル | ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md)を参照してください。
