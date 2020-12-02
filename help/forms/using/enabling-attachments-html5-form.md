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


# HTML5フォームの添付ファイルの有効化  {#enabling-attachments-for-an-html-form}

HTML5フォームでは、添付ファイルをアップロード、プレビューおよび送信することができます。デフォルトでは、添付ファイルサポートは無効になっています。添付ファイルサポートを有効にするには：

1. [ 文字列プロパティで](/help/forms/using/custom-profile.md)カスタムプロファイル`mfAttachmentOptions`を作成します。
1. カスタムプロファイルで、`fileSizeLimit`、`multiSelect`および`buttonTex`tのプロパティを指定して、添付ファイルウィジェットのオプションを設定します。 必要に応じて、さらに多くのカスタムプロパティを指定することもできます。

1. カスタムプロファイルでは、次の設定を使用します。

   * **multiSelect**-> trueまたはfalse （デフォルトでは true）
   * **fileSizeLimit** -> value_in_mb (say 5) （デフォルトで2 MBs）
   * **buttonText** ->ポップアップウィンドウのボタンテキスト（デフォルトでは「Attach」）
   * **受け入れるファイルタイプを受け入れる（デフォルトでは「audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf」）** 

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 では、指定された制限を超えたサイズのファイルを添付できます。これは既知の問題です。

1. [メタデータエディター](/help/forms/using/manage-form-metadata.md)を使用して、上記でHTML 5フォーム用に作成したカスタムプロファイルを選択します。
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

添付ファイルが有効である場合、HTML5フォームはマルチパート形式のデータを送信します。マルチパート送信データは、**dataXml**&#x200B;と&#x200B;**attachments**&#x200B;の2つの部分で構成されます。

>[!NOTE]
>
>後方互換性を確保するために、`mfAllowAttachments`オプションがオフになっている場合、HTML5フォームはマルチパートデータを送信しません。 **application/xml**&#x200B;形式の単純なデータxmlを送信します。

mfAllowAttachments フラグがオンになっている場合、[送信サービスのプロキシサービス](/help/forms/using/service-proxy.md)もまたマルチパート形式のデータを dataXml と添付ファイルと共に投稿します。
