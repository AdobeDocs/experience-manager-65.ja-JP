---
title: 送信レビュー担当者のフォームへの関連付け
seo-title: Associating submission reviewers with a form
description: AEM Formsで送信レビュー担当者をフォームに関連付ける方法を説明します。 関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。
seo-description: Learn how to associate submission reviewers with a form in AEM Forms. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: Adaptive Forms
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 73%

---

# 送信レビュー担当者とフォームの関連付け {#associating-submission-reviewers-with-a-form}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

フォーム作成時に、フォームポータル経由で送信されたフォームのレビューおよびフィードバックを行うユーザーを指定できます。組織はフィードバックを収集し、送信済みフォームに対して再作業を行うことができます。

AEM Forms では、レビュー担当者グループをフォームに関連付けることができます。フォームのレビューグループに追加されたユーザーは、フォームの送信を確認し、フィードバックを提供します。

フォームに割り当てられたレビュー担当者グループは指定されたフォームのみをレビューできます。

## 前提条件 {#prerequisite}

### メタデータスキーマエディターを使用してアダプティブフォームの送信レビュー担当者グループプロパティを有効にする {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

レビュー担当者グループをフォームに関連付けるには、アダプティブフォームのメタデータスキーマを編集します。 デフォルトでは、送信されたフォームにレビュー担当者グループを追加できません。

メタデータスキーマを編集するには、以下の手順に従います。

1. オーサーモードで、Experience Manager の **ツール**／**アセット**／**メタデータスキーマ** をクリックします。
1. スキーマFormsページで、に移動します。 **Forms** > **FormsがAEMで作成されました。**

   ページの URL は以下のとおりです。

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 「**アダプティブフォーム**」を選択し、「**編集**」をクリックします。
1. 「フォームの編集」ページで、「**詳細**」をクリックします。
1. 「詳細」タブで、ビルドフォームで使用可能な「**1 行テキスト**」コンポーネントをドラッグ＆ドロップします。
1. 追加されたテキストコンポーネントを選択し、その設定を確認します。

   「設定」の下の「プロパティにマップ」フィールドに `./jcr:content/metadata/form-submission-reviewer-group` と入力します。

   アダプティブフォームの詳細属性の送信レビュー担当者グループフィールドが、フィールドラベルで指定した名前で有効化されます。

## 送信レビュー担当者のフォームへの関連付け {#associating-submission-reviewers-with-a-form-1}

送信レビュー担当者をアダプティブフォームに関連付けるには、レビュー担当者グループを作成し、そのグループにユーザーを追加します。 フォームの詳細属性内のフォーム送信レビュー担当者のフィールドに、作成したレビュー担当者グループを追加します。ユーザーグループを使用することで、アダプティブフォームごとに異なる送信レビュー担当者のグループを関連付けることができます。この機能によって、権限のないユーザーによる送信レビューを避けることができます。

以下の手順を行う前に、「[必要条件](../../forms/using/adding-reviewers-form.md#prerequisite)」を参照してください。

グループを作成し、メンバーを追加するには、**ツール**／**操作**／**セキュリティ**／**グループ**&#x200B;に移動します。詳しくは、「[ユーザー管理およびサービス](/help/sites-administering/security.md)」を参照してください。作成したグループが、あらかじめ用意されているユーザーグループ **forms-submission-reviewers** のメンバーとして追加されていることを確認してください。このユーザーグループは、AEM Forms に付属しており、ユーザーは送信レビュー担当者として確実に追加されます。

ユーザーグループをアダプティブフォームに関連付けるには、次の手順を実行します。

1. 作成者モードで、**フォーム**／**フォームとドキュメント**&#x200B;に移動します。
1. 「**選択**」オプションを使用してアダプティブフォームを選択し、「**プロパティを表示**」をクリックします。
1. フォームのプロパティウィンドウで「**編集**」をクリックし、「**詳細**」をクリックします。
1. 送信レビュー担当者グループのフィールドにグループを入力し、「**完了**」をクリックします。

   送信レビュー担当者グループのフィールドには、アダプティブフォームのメタデータスキーマの編集で指定した名前が表示されます。

>[!NOTE]
>
>AEM Formsのリモート実装でユーザーとフォームを確実に使用できるように、ユーザーとフォームを複製します。
>
>リモートで、すべてのユーザーがレビュー担当のメンバーとして複製されていることを確認してください。
