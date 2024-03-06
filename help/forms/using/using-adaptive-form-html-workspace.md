---
title: HTML Workspace でのアダプティブフォームの使用
description: フィールドワーカーがデバイス上のフォームにアクセスできるようにする、HTMLワークスペースでのアダプティブフォームの使用方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 44%

---

# HTML Workspace でのアダプティブフォームの使用{#using-an-adaptive-form-in-html-workspace}

JEE 上のAEM Formsには、Workspace でアダプティブフォームを使用する機能が用意されています。HTML

プロセスデザインの際に XDP を選択できるため、既存のアダプティブフォーム AEM リポジトリから参照できる機能が追加されました。この機能により、プロセスデザイナーは、アダプティブフォームを Starting Point および Task 内で設定できます。

## プロセスデザインエクスペリエンス {#process-design-experience}

プロセスデザインでアダプティブフォームを使用できるようにするには、次の手順を実行します。

* タスクの割り当てとスタートポイントでは、CRX リポジトリ内のアダプティブフォームアセットを参照して、タスクにフォームアセットを割り当てることができます。
* 「Assign Task」/「Start Point」Workbench プロパティシートで、アダプティブフォームの最上位/グローバルツールバーを非表示にすることができます。
* アダプティブフォームで、レンダリングアクションと送信アクションに新しいアクションプロファイルを使用することができます。

### LiveCycleアプリケーションの書き出しと読み込み {#livecycle-application-export-and-import}

アダプティブフォームはAEMリポジトリ内にあるので、LiveCycleの書き出しには、使用するアダプティブフォームの参照のみが含まれます。 そのため、LiveCycle アプリケーションのエクスポートおよびインポートは、2 段階のプロセスとなっています。LiveCycleアプリケーションには、プロセスの定義などが含まれます。 アダプティブフォームを含む別のパッケージが、AEMから ZIP ファイルとして書き出されます。 読み込み時に、LiveCycleアプリケーションは Workbench を通じて読み込まれ、アダプティブフォームはAEMを通じて読み込まれます。

## Workspace でのアダプティブフォームのユーザーエクスペリエンスHTML {#user-experience-of-adaptive-form-in-html-workspace}

HTMLWorkspace には、モバイルフォームで使用できるコントロールに加えて、アダプティブフォーム固有のコントロールがいくつか用意されています。 Task または Start Point を開くと、HTMLWorkspace でアダプティブフォームの添付ファイルの追加、保存、署名、送信、ナビゲーションを行うことができます。 詳細は次のとおりです。

1. ファイルを添付するには、Mobile Formsと同様に、タスクの添付ファイルを使用します。 アダプティブフォームでは、File Attachment タイプのボタンは非表示になっています。

1. アダプティブフォームを保存するには、Mobile Forms の場合と同じように「**保存**」をクリックします。アダプティブフォームでは、Save タイプのボタンは非表示になっています。

1. アダプティブフォームを送信するには、Mobile Forms と同じように、「**送信**」ボタンを使うか、またはルートアクションを使用します。アダプティブフォームでは、Submit タイプのボタンは非表示になっています。

1. **アダプティブフォームのグローバルツールバーの表示**：プロセスデザイナーでグローバル/トップレベルのツールバーが非表示になっている場合は、ツールバーとボタンがアダプティブフォームに表示されません。

1. **Workspace でのアダプティブフォームのナビゲーションコントロール**：HTML Workspace のアダプティブフォームでは、「保存」、「送信」、「ルートアクション」のボタンに加え、「次へ」／「前へ」ボタンも使用できます。次へ/前へボタンをクリックすると、Workspace でアダプティブフォームのパネルを移動することができますHTML。 「次へ」／「前へ」ボタンは、アダプティブフォームのモバイル表示のナビゲーションコントロールのような、精密なナビゲーションを提供します。

1. **アダプティブフォームの eSign サービスと Summary コンポーネント**：Summary コンポーネントは、HTML Workspace では操作できません。つまり、アダプティブフォームに Summary コンポーネントが含まれている場合、Workspace には表示されません。 E 署名コンポーネントでは、自動送信の代わりに、Workspace ユーザーは Workspace で送信またはルートアクションをクリックします。HTML ドキュメントに署名した後は、フラットな署名済みドキュメントとして表示されます。 クリック **送信** またはルートアクションを使用して、タスクまたはスタートポイントを閉じたり、完了したりできます。\
   署名済みのドキュメントが eSign サービスサーバーから収集され、データ xml ファイルがプロセス内の次のステップへと転送されます。

## アダプティブフォームをプロセスデザインで使用するための手順 {#steps-to-use-adaptive-forms-in-process-design}

1. Adobe Experience Manager Forms Workbench を開きます。

1. **ファイル／新規／アプリケーション**&#x200B;に移動するか、または既存のアプリケーションを使用してアプリケーションを作成します。

   ![新しいアプリケーションの作成](assets/create_new_appl.png)

   アプリケーションの作成

1. プロセスを作成するか、またはアプリケーション内の既存のプロセスを使用します。

   ![新しいプロセスの作成](assets/create_new_process.png)

   プロセスを作成

1. Start Point または Assign Task を作成し、ダブルクリックします。
1. 「**[!UICONTROL プレゼンテーションとデータ]**」セクションで、「**[!UICONTROL CRX アセットを使用]**」を選択し、アセットの前にある省略記号をクリックします。

   ![CRX アセットを使用](assets/use_crx_asset.png)

   CRX アセットを使用

1. アセットを管理 UI を通して作成されたアダプティブフォームを選択し、「**[!UICONTROL OK]**」をクリックします。

   ![アダプティブフォームの選択](assets/selecting_form.png)

   アダプティブフォームを選択します

   >[!NOTE]
   >
   >アダプティブフォームの作成について詳しくは、 [アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md).
   >
   >
   >プロセスの作成について詳しくは、[プロセスの作成と管理](https://help.adobe.com/ja_JP/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)を参照してください。
