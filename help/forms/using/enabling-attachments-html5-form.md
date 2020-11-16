---
title: HTML5フォームの添付ファイルの有効化
seo-title: HTML5フォームの添付ファイルの有効化
description: デフォルトでは、HTML5フォームの添付ファイルサポートは無効になっています。
seo-description: デフォルトでは、HTML5フォームの添付ファイルサポートは無効になっています。
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 62%

---


# HTML5フォームの添付ファイルの有効化 {#enabling-attachments-for-an-html-form}

HTML5フォームでは、添付ファイルをアップロード、プレビューおよび送信することができます。デフォルトでは、添付ファイルサポートは無効になっています。添付ファイルサポートを有効にするには：

1. [ 文字列プロパティで](/help/forms/using/custom-profile.md)カスタムプロファイル`mfAttachmentOptions`を作成します。
1. In the custom profile, specify properties `fileSizeLimit`, `multiSelect`, and `buttonTex`t to configure options of the file attachment widget. 必要に応じて、さらに多くのカスタムプロパティを指定することもできます。

1. カスタムプロファイルでは、次の設定を使用します。

   * **multiSelect**-> trueまたはfalse （デフォルトでは true）
   * **fileSizeLimit** -> value_in_mb (say 5) （デフォルトで2 MBs）
   * **buttonText** ->ポップアップウィンドウのボタンテキスト（デフォルトでは「Attach」）
   * **accept** ->受け入れるファイルタイプ（デフォルトでは「audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf」）

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 では、指定された制限を超えたサイズのファイルを添付できます。これは既知の問題です。

1. Use the [metadata editor](/help/forms/using/manage-form-metadata.md) to select the custom profile that you have created above for HTML 5 forms.
1. カスタムプロファイルを使用してフォームテンプレートをレンダリングすると、添付ファイルアイコンがフォームツールバーの上に表示されます。

   >[!NOTE]
   >
   >ドラフトと添付ファイル機能を有効にすると、フォームポータルはデフォルトで、ファイルカスタムプロファイルを提供します。**ドラフトとして保存**&#x200B;プロファイルに関する詳細は、[HTML5 フォームをドラフトとして保存](/help/forms/using/saving-html5-form-draft.md)を参照してください。

1. 添付ファイルアイコンをクリックすると、添付ファイル選択ダイアログボックスが表示されます。ファイルを参照して添付ファイルを選択して&#x200B;**「添付」**&#x200B;をクリックします。

   >[!NOTE]
   >
   >添付ファイルをプレビューするには、添付ファイル名をクリックします。

   >[!NOTE]
   >
   >匿名のユーザーは、ファイルプレビューオプションを使用できません。

## 添付ファイル送信フォーマット {#attachment-submission-format}

添付ファイルが有効である場合、HTML5フォームはマルチパート形式のデータを送信します。The multi-part submission data has two parts **dataXml** and **attachments**.

>[!NOTE]
>
>For backward compatibility, if `mfAllowAttachments` option is turned off, then the HTML5 forms does not send the multi-part data. It sends simple data xml in **application/xml** format.

mfAllowAttachments フラグがオンになっている場合、[送信サービスのプロキシサービス](/help/forms/using/service-proxy.md)もまたマルチパート形式のデータを dataXml と添付ファイルと共に投稿します。
