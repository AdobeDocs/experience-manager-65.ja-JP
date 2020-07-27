---
title: フォームへの送信レビュー担当者の関連付け
seo-title: フォームへの送信レビュー担当者の関連付け
description: AEM Forms のフォームへ送信レビュー担当者を関連付ける方法を説明します。関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
seo-description: AEM Forms のフォームへ送信レビュー担当者を関連付ける方法を説明します。関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 69%

---


# フォームへの送信レビュー担当者の関連付け {#associating-submission-reviewers-with-a-form}

フォーム作成時に、フォームポータル経由で送信されたフォームのレビューおよびフィードバックを行うユーザーを指定することができます。組織はフィードバックを収集し、送信済みフォームに対して再作業を行うことができます。

AEM Forms では、レビュー担当者グループをフォームへ関連付けることができます。フォームのレビューグループに追加されたユーザーは、このフォームの送信を確認し、フィードバックを提供します。

フォームに割り当てられたレビュー担当者グループは指定されたフォームのみをレビューできます。

## 前提条件 {#prerequisite}

### メタデータスキーマエディターを使用してアダプティブフォームで送信レビュー担当者グループのプロパティを有効化 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

レビュー担当者グループをフォームに関連付けるには、アダプティブフォームのメタデータスキーマを編集します。デフォルトでは、送信されたフォームにレビュー担当者グループを追加することはできません。

メタデータスキーマを編集するには、次の手順に従います。

1. 作成者モードを使用して、Experience Manager の「**ツール**／**アセット**／**メタデータスキーマ**」をクリックします。
1. スキーマフォームページで、「**フォーム**／**AEM で作成されたフォーム**」に移動します。

   ページのURLは次のとおりです。

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Select **Adaptive Form** and click **Edit**.
1. 「フォームの編集」ページで、「**詳細**」をクリックします。
1. In the Advanced tab, drag-and-drop the **Single Line Text** component available under Build Form.
1. 追加されたテキストコンポーネントを選択し、その設定を確認します。

   「設定」の下の「プロパティ `./jcr:content/metadata/form-submission-reviewer-group` にマップ」フィールドにと入力します。

   アダプティブフォームの詳細属性の送信レビュー担当者グループフィールドが、フィールドラベルで指定した名前で有効化されます。

## フォームへの送信レビュー担当者の関連付け {#associating-submission-reviewers-with-a-form-1}

アダプティブフォームに送信レビュー担当者を関連付けるには、レビュー担当者グループを作成し、そこにユーザーを追加します。フォームの詳細属性内のフォーム送信レビュー担当者のフィールドに、作成したレビュー担当者グループを追加します。ユーザーグループを使用することで、アダプティブフォームごとに異なる送信レビュー担当者のグループを関連付けることができます。この機能は、権限のないユーザーによる送信レビューを防止します。

以下の手順を行う前に、「[必要条件](../../forms/using/adding-reviewers-form.md#prerequisite)」を参照してください。

To create a group and add members to it, navigate to **Tools** > **Operations** > **Security** > **Groups**.
For more information, see [User Administration and Services](/help/sites-administering/security.md).
Ensure that you add the group you create as a member of the out-of-the-box user group: **forms-submission-reviewers**. このユーザーグループはAEM Formsに付属しており、送信レビュー担当者として追加されていることを確認します。

アダプティブフォームにユーザーグループを関連付けるには、次の手順に従います。

1. 作成者モードで、「**フォーム**／**フォームとドキュメント**」に移動します。
1. Use the **Select **option to select an adaptive form, and click **View Properties**.
1. In the Properties window of the form, click **Edit**, and then click **ADVANCED**.
1. Enter the group in the submission reviewer group field, and click **Done**.

   送信レビュー担当者グループのフィールドには、アダプティブフォームのメタデータスキーマの編集で指定した名前が表示されます。

>[!NOTE]
>
>リモートでの AEM Forms の導入においてユーザーとフォームの可用性を確認するには、ユーザーとフォームを複製してください。
>
>リモートで、すべてのユーザーがレビュー担当のメンバーとして複製されていることを確認してください。

