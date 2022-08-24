---
title: HTML Workspace でのアダプティブフォームの使用
seo-title: Using an adaptive form in HTML Workspace
description: HTML Workspace でのアダプティブフォームの使用
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 100%

---

# HTML Workspace でのアダプティブフォームの使用{#using-an-adaptive-form-in-html-workspace}

JEE 上の AEM Forms では、HTML Workspace でアダプティブフォームを使用することができます。

プロセスデザインの際に XDP を選択することができるため、既存のアダプティブフォーム AEM レポジトリから参照できる機能が追加されました。この機能により、プロセスデザイナーは、アダプティブフォームを Task からだけでなく、Starting Point からも設定することができます。

## プロセスデザインのエクスペリエンス {#process-design-experience}

プロセスデザインでアダプティブフォームの使用を有効化するには、次の手順を実行します。

* 「Assign Task」および「Start Point」では、タスクにフォームアセットを割り当てる際に、CRX リポジトリ内のアダプティブフォームアセットを参照することができます。
* 「Assign Task」および「Start Point」の Workbench プロパティシートでは、アダプティブフォームのトップレベル / グローバルツールバーを非表示にすることができます。
* 新しいアクションプロファイルを、アダプティブフォームでのレンダリングおよび送信アクションに使用することができます。

### LiveCycle アプリケーションのエクスポートおよびインポート {#livecycle-application-export-and-import}

アダプティブフォームは AEM リポジトリにあるため、LiveCycle アプリケーションのエクスポートには、使用されているアダプティブフォームへのリファレンスのみが含まれています。そのため、LiveCycle アプリケーションのエクスポートおよびインポートは、2 段階のプロセスとなっています。LiveCycle アプリケーションには、プロセスの定義などが含まれています。アダプティブフォームを含む別のパッケージが、AEM より ZIP ファイルにてエクスポートされます。インポート中、LiveCycle アプリケーションは Workbench を通してインポートされ、アダプティブフォームは AEM を通してインポートされます。

## HTML Workspace におけるアダプティブフォームのユーザーエクスペリエンス {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace は、モバイルフォームに使用できるコントロールのほかに、アダプティブフォーム特有のコントロールをいくつか提供しています。HTML Workspace で「Task」または「Start Point」を開くと、ユーザーは、アダプティブフォームをナビゲートし、保存、署名、送信、添付ファイルの追加を行うことができます。詳しい内容は次のとおりです。

1. ファイルを添付するには、Mobile Forms と同じように、「Task」の添付ファイルを使用します。アダプティブフォームでは、File Attachment タイプのボタンは非表示になっています。

1. アダプティブフォームを保存するには、Mobile Forms の場合と同じように「**保存**」をクリックします。アダプティブフォームでは、Save タイプのボタンは非表示になっています。

1. アダプティブフォームを送信するには、Mobile Forms と同じように、「**送信**」ボタンを使うか、またはルートアクションを使用します。アダプティブフォームでは、Submit タイプのボタンは非表示になっています。

1. **アダプティブフォームグローバルツールバーの表示**：プロセスデザイナーがグローバル / トップレベルツールバーを非表示にした場合、ツールバーおよびボタンはアダプティブフォームに表示されません。

1. **Workspace でのアダプティブフォームのナビゲーションコントロール**：HTML Workspace のアダプティブフォームでは、「保存」、「送信」、「ルートアクション」のボタンに加え、「次へ」／「前へ」ボタンも使用できます。HTML Workspace でアダプティブフォームのパネルをナビゲートするには、「次へ」／「前へ」ボタンをクリックします。「次へ」／「前へ」ボタンは、アダプティブフォームのモバイル表示のナビゲーションコントロールのような、精密なナビゲーションを提供します。

1. **アダプティブフォームの eSign サービスと Summary コンポーネント**：Summary コンポーネントは、HTML Workspace では操作できません。つまり、アダプティブフォームに Summary コンポーネントが含まれていても、ワークスペースでは表示されません。HTML Workspace では、ユーザーは、Esign コンポーネントの自動送信の代わりに、送信またはルートアクションをクリックします。ドキュメントが署名された後は、フラット（非インタラクティブ）な署名済みドキュメントとして表示されます。「**送信**」またはルートアクションをクリックして、タスクまたは Start Point を閉じます。\
   署名済みのドキュメントが eSign サービスサーバーから収集され、データ xml ファイルがプロセス内の次のステップへと転送されます。

## アダプティブフォームをプロセスデザインで使用するための手順 {#steps-to-use-adaptive-forms-in-process-design}

1. Adobe Experience Manager Forms Workbench を開きます。

1. **ファイル／新規／アプリケーション**&#x200B;に移動するか、または既存のアプリケーションを使用してアプリケーションを作成します。

   ![新しいアプリケーションの作成](assets/create_new_appl.png)

   新しいアプリケーションの作成

1. プロセスを作成するか、またはアプリケーション内の既存のプロセスを使用します。

   ![新しいプロセスの作成](assets/create_new_process.png)

   新しいプロセスの作成

1. Start Point または Assign Task を作成し、ダブルクリックします。
1. 「**[!UICONTROL プレゼンテーションとデータ]**」セクションで、「**[!UICONTROL CRX アセットを使用]**」を選択し、アセットの前にある省略記号をクリックします。

   ![CRX アセットを使用](assets/use_crx_asset.png)

   CRX アセットを使用

1. アセットを管理 UI を通して作成されたアダプティブフォームを選択し、「**[!UICONTROL OK]**」をクリックします。

   ![アダプティブフォームの選択](assets/selecting_form.png)

   アダプティブフォームの選択

   >[!NOTE]
   >
   >アダプティブフォームの作成について詳しくは、「[アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md)」を参照してください。
   >
   >
   >プロセスの作成について詳しくは、[プロセスの作成と管理](https://help.adobe.com/ja_JP/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)を参照してください。
