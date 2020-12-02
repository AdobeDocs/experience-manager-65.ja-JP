---
title: HTML Workspace でのアダプティブフォームの使用
seo-title: HTML Workspace でのアダプティブフォームの使用
description: HTML Workspace でのアダプティブフォームの使用
seo-description: HTML Workspace でのアダプティブフォームの使用
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 70%

---


# HTML Workspace でのアダプティブフォームの使用{#using-an-adaptive-form-in-html-workspace}

JEE上のAEM Formsは、HTML Workspaceでアダプティブフォームを使用する機能を提供します。

プロセスデザイン中にXDPを選択できるので、既存のアダプティブフォームAEMリポジトリから参照する機能が追加されました。 この機能により、プロセスデザイナーはアダプティブフォームをスタートポイントやタスクで設定することができます。

## プロセスデザインのエクスペリエンス {#process-design-experience}

プロセスデザインでアダプティブフォームの使用を有効化するには、次の手順を実行します。

* 「Assign Task」および「Start Point」では、タスクにフォームアセットを割り当てる際に、CRX リポジトリ内のアダプティブフォームアセットを参照することができます。
* 「Assign Task」および「Start Point」の Workbench プロパティシートでは、アダプティブフォームのトップレベル / グローバルツールバーを非表示にすることができます。
* 新しいアクションプロファイルを、アダプティブフォームでのレンダリングおよび送信アクションに使用することができます。

### LiveCycle アプリケーションのエクスポートおよびインポート  {#livecycle-application-export-and-import}

アダプティブフォームは AEM リポジトリにあるため、LiveCycle アプリケーションのエクスポートには、使用されているアダプティブフォームへのリファレンスのみが含まれています。したがって、LiveCycleアプリの書き出しと読み込みは、2つの手順で行います。 LiveCycle アプリケーションには、プロセスの定義などが含まれています。アダプティブフォームを含む別のパッケージが、AEM より ZIP ファイルにてエクスポートされます。インポート中、LiveCycle アプリケーションは Workbench を通してインポートされ、アダプティブフォームは AEM を通してインポートされます。

## HTML Workspace におけるアダプティブフォームのユーザーエクスペリエンス  {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace は、モバイルフォームに使用できるコントロールのほかに、アダプティブフォーム特有のコントロールをいくつか提供しています。HTML Workspace で「Task」または「Start Point」を開くと、ユーザーは、アダプティブフォームをナビゲートし、保存、署名、送信、添付ファイルの追加を行うことができます。詳しい内容は次のとおりです。

1. ファイルを添付するには、Mobile Forms と同じように、添付ファイルタスクをします。アダプティブフォームでは、File Attachment タイプのボタンは非表示になっています。

1. アダプティブフォームを保存するには、「**保存**」をクリックします。アダプティブフォームでは、Save タイプのボタンは非表示になっています。

1. アダプティブフォームを送信するには、Mobile Forms と同じように、「**送信**」ボタンを使うか、またはルートアクションを使用します。アダプティブフォームでは、Submit タイプのボタンは非表示になっています。

1. **アダプティブフォームグローバルツールバーの表示**:プロセスデザイナーがグローバル/トップレベルのツールバーを非表示にした場合、ツールバー、ボタンはアダプティブフォームに表示されません。

1. **アダプティブFormsのWorkspaceナビゲーションコントロール**:HTML Workspaceのアダプティブフォームでは、次へ/前へのボタンを、保存、送信、ルートアクションのボタンと共に使用できます。HTML Workspace でアダプティブフォームのパネルをナビゲートするには、次へ / 前へのボタンをクリックします。次へ／前へのボタンは、アダプティブフォームのモバイル表示のナビゲーションコントロールに似た精密なナビゲーションを提供します。

1. **アダプティブフォームのeSignサービスとSummaryコンポーネント**:Summaryコンポーネントは、HTML Workspaceでは操作できません。つまり、アダプティブフォームに Summary コンポーネントが含まれていても、ワークスペースでは表示されません。HTML Workspace では、ユーザーは、Esign コンポーネントの自動送信の代わりに、送信またはルートアクションをクリックします。ドキュメントが署名された後は、フラット（非インタラクティブ）な署名済みドキュメントとして表示されます。「**送信**」またはルートアクションをクリックして、タスクまたは Start Point を閉じます。\
   署名済みのドキュメントが eSign サービスサーバーから収集され、データ xml ファイルがプロセス内の次のステップへと転送されます。

## アダプティブフォームをプロセスデザインで使用するための手順 {#steps-to-use-adaptive-forms-in-process-design}

1. Adobe Experience Manager Forms Workbench を開きます。

1. **File/New/Application**&#x200B;に移動するか、既存のアプリケーションを使用してアプリケーションを作成します。

   ![新しいアプリケーションの作成](assets/create_new_appl.png)

   新しいアプリケーションの作成

1. プロセスを作成するか、アプリケーション内の既存のプロセスを使用します。

   ![新しいプロセスの作成](assets/create_new_process.png)

   新しいプロセスの作成

1. 開始ポイントを作成するか、タスクを割り当て、重複をクリックします。
1. **[!UICONTROL Presentation &amp; Data]** セクションで、**[!UICONTROL CRX アセットの使用]**&#x200B;を選択し、アセットの前の三点リーダーをクリックします。

   ![CRX アセットを使用する](assets/use_crx_asset.png)

   CRX アセットを使用する

1. 「アセットを管理」UIで作成したアダプティブフォームを選択し、「**[!UICONTROL OK]**」をクリックします。

   ![アダプティブフォームの選択](assets/selecting_form.png)

   アダプティブフォームの選択

   >[!NOTE]
   >
   >アダプティブフォームの作成について詳しくは、「[アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md)」を参照してください。
   >
   >
   >プロセスの作成について詳しくは、[プロセスの作成と管理](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)を参照してください。

