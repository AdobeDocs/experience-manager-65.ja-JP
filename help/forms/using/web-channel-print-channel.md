---
title: 印刷チャネルと Web チャネル
description: 印刷チャネルテンプレートを読み込み、web チャネルテンプレートを作成して有効にする
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '696'
ht-degree: 100%

---

# 印刷チャネルと Web チャネル{#print-channel-and-web-channel}

インタラクティブ通信は、印刷チャネルと web チャネルという 2 つのチャネルを使用して配信することができます。印刷チャネルは、PDF や紙ベースの通信手段（保険料の支払いを通知する印刷書類など）を作成する場合に使用され、web チャネルは、オンライン情報（web サイト上で表示されるクレジットカードの取引明細など）を配信する場合に使用されます。

インタラクティブ通信の作成者は、ドキュメントフラグメントや画像などのアセットを再利用して、印刷バージョンと web バージョンの両方でインタラクティブ通信を作成できます。

[インタラクティブ通信を作成](../../forms/using/create-interactive-communication.md)する場合の前提条件として、印刷チャネルまたは web チャネル（またはその両方）のテンプレートがサーバー上に存在している必要があります。テンプレートの作成者は、AEM で web チャネルのテンプレートを作成できますが、印刷チャネルテンプレート（XDP）は Adobe Forms Designer で作成して、サーバーにアップロードします。

## 印刷チャネル {#printchannel}

印刷チャネルのインタラクティブ通信では、XFA フォームのテンプレートである XDP を使用します。XDP は Adobe Forms Designer でデザインします。印刷チャネルのテンプレートを作成する方法については、[レイアウトデザイン](../../forms/using/layout-design-details.md)を参照してください。インタラクティブ通信内で印刷チャネルのテンプレートを使用するには、そのテンプレートを AEM Forms サーバーにアップロードする必要があります。

### インタラクティブ通信の印刷チャネルテンプレートをアップロードする {#upload-interactive-communication-print-channel-template}

テンプレートをアップロードするには、forms-user グループのメンバーになっている必要があります。印刷チャネルテンプレート（XDP）を AEM Forms にアップロードするには、以下の手順を実行します。

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルをアップロード]**&#x200B;を選択します。

   目的の印刷チャネルテンプレート（XDP）に移動して選択し、「**[!UICONTROL 開く]**」を選択します。

## web チャネル {#web-channel}

テンプレートの作成者と管理者は、web テンプレートの作成、編集、有効化を行うことができます。それ以外のユーザーが web テンプレートを作成できるようにするには、そのユーザーに対して権限を設定する必要があります。詳しくは、[ユーザー、グループ、アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md)を参照してください。

### web チャネルテンプレートの作成 {#authoring-web-channel-template}

web チャネルテンプレートを作成するには、最初にテンプレートフォルダーを作成する必要があります。テンプレートフォルダー内に web チャネルテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、Forms ユーザーがそのテンプレートを使用して、インタラクティブ通信の web チャネルを作成できるようになります。

Web チャネルテンプレートを作成するには、以下の手順を実行します。

1. インタラクティブ通信の web チャネルテンプレートを保存するためのテンプレートフォルダーを作成します（まだ作成されていない場合）。詳しくは、[編集可能なページテンプレート](/help/sites-developing/page-templates-editable.md)の「テンプレートフォルダー」を参照してください。

   1. **[!UICONTROL ツール]** ![ツール](assets/tools.png)／**[!UICONTROL 設定ブラウザー]**&#x200B;を選択します。
      * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
   1. 設定ブラウザーページで、「**[!UICONTROL 作成]**」を選択します。
   1. 設定作成ダイアログでフォルダーのタイトルを入力し、「**[!UICONTROL 編集可能テンプレート]**」を選択して「**[!UICONTROL 作成]**」を選択します。

      フォルダーが作成され、設定ブラウザーのページに表示されます。

1. 目的のテンプレートフォルダーに移動して、web テンプレートを作成します。

   1. **[!UICONTROL ツール]**／**[!UICONTROL テンプレート]**／**`[Folder]`** を選択して、目的のテンプレートフォルダーに移動します。
   1. 「**[!UICONTROL 作成]**」を選択します。
   1. 「**[!UICONTROL インタラクティブ通信 - web チャネル]**」を選択して「**[!UICONTROL 次へ]**」を選択します。
   1. テンプレートのタイトルと説明を入力して「**[!UICONTROL 作成]**」を選択します。

      テンプレートが作成されダイアログが表示されます。

   1. 「**[!UICONTROL 開く]**」を選択して、作成したテンプレートをテンプレートエディターで開きます。

      テンプレートエディターが表示されます。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      テンプレートの作成者は、テンプレートの作成や編集を行う際に、様々な要素を定義することができます。テンプレートの作成と編集は、ページの作成に似ています。詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)の「テンプレートの編集 - テンプレート作成者」を参照してください。

1. このテンプレートを使用してインタラクティブ通信を作成できるようにするには、このテンプレートを有効にします。

   1. **[!UICONTROL ツール]** ![ツール](assets/tools.png)／**[!UICONTROL テンプレート]**&#x200B;を選択します。
   1. 目的のテンプレートに移動して選択し、「**[!UICONTROL 有効]**」を選択してから、アラートメッセージ内の「**[!UICONTROL 有効]**」を選択します。

      これでテンプレートが有効になり、テンプレートのステータスとして「有効」が表示されます。これで、新しく作成した web チャネルテンプレートを使用して、インタラクティブ通信を作成することができます。

### 印刷チャネルを web チャネルのプライマリとして使用する {#print-channel-as-master-for-web-channel}

インタラクティブ通信を作成する際に、このオプションを選択すると、印刷チャネルと同期した eb チャネルを作成することができます。印刷チャネルを web チャネルのプライマリとして使用すると、web チャネルのコンテンツ、継承、データバインディングが印刷チャネルから取得され、印刷チャネルでの変更内容が web チャネルに反映されます。ただし、インタラクティブ通信の作成者は、必要に応じて、web チャネル内の特定のコンポーネントの継承を解除することができます。

![印刷チャネルをマスターとして使用](assets/create_ic_print_master_new.png) ![印刷チャネルをマスターとする web チャネル](assets/create_ic_print_master_web_new.png)
