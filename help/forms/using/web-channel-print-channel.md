---
title: 印刷チャネルと Web チャネル
seo-title: 印刷チャネルと Web チャネル
description: 印刷チャネルテンプレートを読み込み、Web チャネルテンプレートを作成して有効にする
seo-description: 印刷チャネルテンプレートを読み込み、Web チャネルテンプレートを作成して有効にする
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 53%

---


# 印刷チャネルと Web チャネル{#print-channel-and-web-channel}

インタラクティブ通信は、印刷チャネルと Web チャネルという 2 つのチャネルを使用して配信することができます。印刷チャネルは、PDF や紙ベースの通信手段（保険料の支払いを通知する印刷書類など）を作成する場合に使用され、Web チャネルは、オンライン情報（Web サイト上で表示されるクレジットカードの取引明細など）を配信する場合に使用されます。

Interactive Communicationの作成者は、ドキュメントフラグメントや画像などのアセットを再利用して、印刷版とWeb版の両方のInteractive Communicationを作成できます。

[Creating an Interactive Communication](../../forms/using/create-interactive-communication.md)の前提条件の1つは、印刷やWebチャネル用のテンプレートをサーバーで使用できるようにすることです。 テンプレート作成者は、AEM自体でWebチャネルテンプレートを作成しますが、印刷チャネルテンプレートXDPはAdobeFormsデザイナーで作成され、サーバーにアップロードされます。

## 印刷チャネル {#printchannel}

Interactive Communicationの印刷チャネルは、XFAフォームテンプレートXDPを使用します。 XDP は Adobe Forms Designer でデザインできます。印刷チャネルテンプレートの作成について詳しくは、[レイアウトデザイン](../../forms/using/layout-design-details.md)を参照してください。 Interactive Communicationで印刷チャネルテンプレートを使用するには、テンプレートをAEM Formsサーバにアップロードする必要があります。

### インタラクティブ通信の印刷チャネルテンプレートのアップロード {#upload-interactive-communication-print-channel-template}

テンプレートをアップロードするには、forms-user グループのメンバーになっている必要があります。印刷チャネルテンプレート（XDP）を AEM Forms にアップロードするには、以下の手順を実行します。

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. **[!UICONTROL 作成]**／**[!UICONTROL ファイルのアップロード]**&#x200B;の順にタップします。

   適切な印刷チャネルテンプレート(XDP)に移動して選択し、「**[!UICONTROL 開く]**」をタップします。

## Web チャネル {#web-channel}

テンプレートの作成者と管理者は、テンプレートの作成、編集、有効化を行うことができます。それ以外のユーザーが Web テンプレートを作成できるようにするには、そのユーザーに対して権限を設定する必要があります。詳しくは、「[ユーザー、グループ、アクセス権の管理](/help/sites-administering/user-group-ac-admin.md)」を参照してください。

### Web チャネルテンプレートの作成 {#authoring-web-channel-template}

Web チャネルテンプレートを作成するには、最初にテンプレートフォルダーを作成する必要があります。テンプレートフォルダー内にWebテンプレートを作成したら、フォームユーザーがテンプレートに基づいてインタラクティブ通信のWebチャネルを作成できるように、テンプレートを有効にする必要があります。

Webチャネルテンプレートを作成するには、次の手順を実行します。

1. Interactive Communication Webテンプレートがまだない場合は、テンプレートフォルダを作成して保存します。 詳しくは、[ページテンプレート — 編集可能](/help/sites-developing/page-templates-editable.md)の「テンプレートフォルダー」を参照してください。

   1. **[!UICONTROL ツール]** ![ツール](assets/tools.png) > **[!UICONTROL 設定ブラウザー]**&#x200B;をタップします。
      * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
   1. 設定ブラウザーページで、「**[!UICONTROL 作成]**」をタップします。
   1. 設定を作成ダイアログで、フォルダーのタイトルを指定し、「**[!UICONTROL 編集可能なテンプレート]**」をオンにして、「**[!UICONTROL 作成]**」をタップします。

      フォルダーが作成され、Configuration Browserページに表示されます。

1. 目的のテンプレートフォルダーに移動して、Web チャネルテンプレートを作成します。

   1. **[!UICONTROL ツール]**/**[!UICONTROL テンプレート]**/**`[Folder]`**&#x200B;を選択して、適切なテンプレートフォルダーに移動します。
   1. 「**[!UICONTROL 作成]**」をタップします。
   1. 「**[!UICONTROL 対話型通信 — Webチャネル]**」を選択し、「**[!UICONTROL 次へ]**」をタップします。
   1. テンプレートのタイトルと説明を入力して「**[!UICONTROL 作成]**」をタップします。

      作成されたテンプレートがダイアログに表示されます。

   1. 「**[!UICONTROL 開く]**」をタップして、作成したテンプレートをテンプレートエディターで開きます。

      テンプレートエディターが表示されます。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      テンプレートの作成者は、テンプレートの作成や編集を行う際に、様々な要素を定義することができます。テンプレートの作成と編集は、ページの作成に似ています。詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md)の「テンプレートの編集 — テンプレート作成者」を参照してください。

1. Interactive Communicationの作成時にこのテンプレートを使用できるようにするには、テンプレートを有効にします。

   1. **[!UICONTROL ツール]** ![ツール](assets/tools.png) > **[!UICONTROL テンプレート]**&#x200B;をタップします。
   1. 適切なテンプレートに移動し、選択して「**[!UICONTROL 有効にする]**」をタップし、警告メッセージで「**[!UICONTROL 有効にする]**」をタップします。

      これでテンプレートが有効になり、テンプレートのステータスとして「有効」が表示されます。新しく作成した Web チャネルテンプレートを使用して、インタラクティブ通信を作成することができます。

### 「印刷チャネルを Web チャネルのマスターとして使用する」オプション{#print-channel-as-master-for-web-channel}

インタラクティブ通信を作成する際に、「印刷チャネルを Web チャネルのマスターとして使用する」オプションを選択すると、印刷チャネルに同期された Web チャネルを作成することができます。印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得され、印刷チャネルに対する変更内容が Web チャネルに反映されます。ただし、インタラクティブ通信の作成者は、必要に応じて、Web チャネル内の特定のコンポーネントの継承設定を解除することができます。

![印刷チャネルをマスターとして](assets/create_ic_print_master_new.png) ![MasterWebチャネルーとして印刷する場合、印刷チャネルはマスターとして使用します](assets/create_ic_print_master_web_new.png)

