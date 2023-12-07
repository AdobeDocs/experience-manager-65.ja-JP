---
title: 印刷チャネルと Web チャネル
description: 印刷チャネルテンプレートの読み込み、Web チャネルテンプレートの作成と有効化
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 44%

---

# 印刷チャネルと Web チャネル{#print-channel-and-web-channel}

インタラクティブ通信は、印刷チャネルと Web チャネルの 2 つのチャネルを通じて配信できます。 印刷チャネルは、保険料の支払いを促す印刷済みレターなどのPDFや紙の通信を作成するために使用され、Web チャネルは、Web サイト上のクレジットカード明細などのオンラインエクスペリエンスを配信するために使用されます。

インタラクティブ通信の作成者は、ドキュメントフラグメントや画像などのアセットを再利用して、印刷バージョンと web バージョンの両方でインタラクティブ通信を作成できます。

[インタラクティブ通信を作成](../../forms/using/create-interactive-communication.md)する場合の前提条件として、印刷チャネルまたは web チャネル（またはその両方）のテンプレートがサーバー上に存在している必要があります。テンプレートの作成者は、AEM で web チャネルのテンプレートを作成できますが、印刷チャネルテンプレート（XDP）は Adobe Forms Designer で作成して、サーバーにアップロードします。

## 印刷チャネル {#printchannel}

印刷チャネルのインタラクティブ通信では、XFA フォームのテンプレートである XDP を使用します。XDP は Adobe Forms Designer でデザインします。印刷チャネルのテンプレートを作成する方法については、[レイアウトデザイン](../../forms/using/layout-design-details.md)を参照してください。インタラクティブ通信内で印刷チャネルのテンプレートを使用するには、そのテンプレートを AEM Forms サーバーにアップロードする必要があります。

### インタラクティブ通信の印刷チャネルテンプレートのアップロード {#upload-interactive-communication-print-channel-template}

テンプレートをアップロードするには、forms-user グループのメンバーである必要があります。 次の手順を使用して、印刷チャネルテンプレート (XDP) をAEM Formsにアップロードします。

1. **[!UICONTROL Forms]**／**[!UICONTROL Forms とドキュメント]**&#x200B;を選択します。

1. 選択 **[!UICONTROL 作成]** > **[!UICONTROL ファイルのアップロード]**.

   適切な印刷チャネルテンプレート (XDP) に移動して選択し、「 」を選択します。 **[!UICONTROL 開く]**.

## Web チャネル {#web-channel}

テンプレート作成者と管理者は、Web テンプレートの作成、編集、有効化をおこなえます。 他のユーザーが Web テンプレートを作成できるようにするには、権限を付与する必要があります。 詳しくは、[ユーザー、グループ、アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md)を参照してください。

### Web チャネルテンプレートのオーサリング {#authoring-web-channel-template}

Web チャネルテンプレートを作成するには、まずテンプレートフォルダーを作成する必要があります。 テンプレートフォルダー内に web チャネルテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、Forms ユーザーがそのテンプレートを使用して、インタラクティブ通信の web チャネルを作成できるようになります。

Web チャネルテンプレートを作成するには、以下の手順を実行します。

1. インタラクティブ通信の web チャネルテンプレートを保存するためのテンプレートフォルダーを作成します（まだ作成されていない場合）。詳しくは、[編集可能なページテンプレート](/help/sites-developing/page-templates-editable.md)の「テンプレートフォルダー」を参照してください。

   1. 選択 **[!UICONTROL ツール]** ![ツール](assets/tools.png) > **[!UICONTROL 設定ブラウザー]**.
      * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
   1. 設定ブラウザーページで、「 」を選択します。 **[!UICONTROL 作成]**.
   1. 設定を作成ダイアログで、フォルダーのタイトルを指定し、「 **[!UICONTROL 編集可能なテンプレート]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL 作成]**.

      フォルダーが作成され、設定ブラウザーのページに表示されます。

1. 目的のテンプレートフォルダーに移動して、web テンプレートを作成します。

   1. **[!UICONTROL ツール]**／**[!UICONTROL テンプレート]**／**`[Folder]`** を選択して、目的のテンプレートフォルダーに移動します。
   1. 「**[!UICONTROL 作成]**」を選択します。
   1. 選択 **[!UICONTROL インタラクティブ通信 — Web チャネル]** を選択し、 **[!UICONTROL 次へ]**.
   1. テンプレートのタイトルと説明を入力し、「 」を選択します。 **[!UICONTROL 作成]**.

      テンプレートが作成されダイアログが表示されます。

   1. 選択 **[!UICONTROL 開く]** をクリックして、作成したテンプレートをテンプレートエディターで開きます。

      テンプレートエディタが表示されます。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      テンプレートを作成または編集する際には、テンプレート作成者が定義できる様々な要素があります。 テンプレートの作成や編集は、ページのオーサリングと似ています。 詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)の「テンプレートの編集 - テンプレート作成者」を参照してください。

1. このテンプレートを使用してインタラクティブ通信を作成できるようにするには、このテンプレートを有効にします。

   1. 選択 **[!UICONTROL ツール]** ![ツール](assets/tools.png) > **[!UICONTROL テンプレート]**.
   1. 適切なテンプレートに移動して選択し、「 」を選択します。 **[!UICONTROL 有効にする]** アラートメッセージで、 **[!UICONTROL 有効にする]**.

      テンプレートが有効になり、そのステータスが「有効」と表示されます。 次に、新しく作成した Web チャネルテンプレートを使用するインタラクティブ通信の作成に進むことができます。

### Web チャネルのマスターとしての印刷チャネル {#print-channel-as-master-for-web-channel}

インタラクティブ通信の作成時に、作成者はこのオプションを選択して、印刷チャネルと同期して Web チャネルを作成できます。 印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルのコンテンツ、継承、データ連結が印刷チャネルから派生し、印刷チャネルで行われた変更が Web チャネルに反映される可能性があります。 ただし、インタラクティブ通信の作成者は、必要に応じて、Web チャネル内の特定のコンポーネントの継承を解除できます。

![印刷チャネルをマスターとして使用](assets/create_ic_print_master_new.png) ![印刷チャネルをマスターとする web チャネル](assets/create_ic_print_master_web_new.png)
