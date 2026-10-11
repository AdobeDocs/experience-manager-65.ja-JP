---
title: HTML5 フォームの添付ファイルの有効化
description: デフォルトでは、HTML5 フォームの添付ファイルサポートは無効になっています。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: HTML5 Forms,Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 94%
---
# HTML5 フォームの添付ファイルの有効化 {#enabling-attachments-for-an-html-form}

HTML5 フォームで添付ファイルをアップロード、プレビューおよび送信できます。 デフォルトでは、添付ファイルサポートは無効になっています。 添付ファイルサポートを有効にするには：

1. `mfAttachmentOptions`複数選択文字列プロパティを持つ[カスタムプロファイル](/help/forms/using/custom-profile.md)を作成してください。 `mfAttachmentOptions` プロパティの各文字列は、ファイル添付ウィジェットのオプションを設定するための `property=value` 形式である必要があります。 `property` および `value` は、次のいずれかの値を持つことができます。

   | プロパティ | 値 |
   |--- |---|
   | multiSelect | trueまたはfalse (デフォルトではtrue) |
   | fileSizeLimit | MB 単位の数（デフォルトは 2 MB）。 例えば、5 を入力します。 |
   | buttonText | ポップアップウィンドウのボタンテキスト（デフォルトでは 「Attach」） |
   | 同意 | 受け入れるファイルタイプのコンマ区切りリスト（「audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf」） |

   次に例を示します。

   ![オプションを設定](assets/mfAttachmentOptions.png)

   必要に応じて、`mfAttachmentOptions` プロパティのその他のカスタムオプションを指定することもできます。

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 では、指定された制限を超えたサイズのファイルを添付できます。 これは既知の問題です。

1. [メタデータエディター](/help/forms/using/manage-form-metadata.md)を使用して、上記で HTML5 のフォームのために作成したカスタムプロファイルを選択します。
1. カスタムプロファイルを使用してフォームテンプレートをレンダリングすると、添付ファイルアイコンがフォームツールバーの上に表示されます。

   >[!NOTE]
   >
   >ドラフトと添付ファイル機能を有効にすると、標準のフォームポータルは、ファイルカスタムプロファイルを提供します。 **ドラフトとして保存**&#x200B;プロファイルに関する詳細は、[HTML5 フォームをドラフトとして保存](/help/forms/using/saving-html5-form-draft.md)を参照してください。

1. 添付ファイルアイコンをクリックすると、添付ファイル選択ダイアログボックスが表示されます。 ファイルを参照して添付ファイルを選択して&#x200B;**「添付」**&#x200B;をクリックします。

   >[!NOTE]
   >
   >添付ファイルをプレビューするには、添付ファイル名をクリックします。

   >[!NOTE]
   >
   >匿名のユーザーは、ファイルプレビューオプションを使用できません。

## 添付ファイル送信形式 {#attachment-submission-format}

添付ファイルが有効である場合、HTML5 フォームはマルチパート形式のデータを送信します。 マルチパート形式で送信するデータには&#x200B;**dataXml**&#x200B;および&#x200B;**添付ファイル**&#x200B;の2つの部分があります。

>[!NOTE]
>
>下位互換性については、`mfAllowAttachments` オプションがオフになっている場合、HTML5 フォームはマルチパート形式のデータを送信しません。 **application/xml**&#x200B;形式の単純なデータ xml を送信します。

mfAllowAttachments フラグがオンになっている場合、[送信サービスのプロキシサービス](/help/forms/using/service-proxy.md)もまたマルチパート形式のデータを dataXml と添付ファイルと共に投稿します。
