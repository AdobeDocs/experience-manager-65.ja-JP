---
title: JEE 上のAEM Formsプロセスにデータを送信するためのAEM Formsの設定
description: フォームデータを処理するために、アダプティブフォームを JEE 上のAEM Formsプロセスと統合します。
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 28%

---

# JEE 上のAEMフォームにフォームデータを送信するためのAEM Formsの設定プロセス{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

アダプティブフォームは、さらに処理するためのデータを JEE 上のAEM Formsプロセスに送信する機能をサポートしています。 JEE 上のAEM Formsプロセスのトリガーを、送信済みフォームから利用可能なデータと共に設定できます。 JEE 上のAEM Formsプロセスにアダプティブフォームを送信するためにAEM Formsインスタンスを有効にするには、次の手順を実行します。

## AEM Forms Server の設定 {#configure-your-aem-forms-server}

次の手順を実行して、AEM Forms Server が JEE 上のAEM Formsサーバーにデータを送信できるようにします。

1. AEM web コンソールの設定ページ（https://[*host*]:[*port*]/system/console/configMgr）に移動します。

1. **Adobe LiveCycle Client SDK Configuration** コンポーネントを見つけてクリックします。
1. JEE 上のAEM Formsサーバーの設定サーバー URL、ユーザー名、パスワードをクリックして編集します。
1. 設定を確認し、「**保存**」をクリックします。

![Adobe LiveCycle Client SDK 設定](assets/clientsdkconfiguration.jpg)

## LiveCycle プロセスのフィールドへのデータのマッピング {#map-data-with-process-fields}

AEM Formsの設定後、送信済みフォームのデータ XML と添付ファイルを、JEE 上のAEM Formsプロセスのフィールドにマッピングします。 次の手順を実行します。

1. AEM Web 設定コンソールで、「 」をクリックして **ガイドLiveCycleプロセスロケーターと呼び出し元** 設定。
1. 以下のパラメーターを指定します。

   * **データ xml パラメーターの名前** （必須）:送信されたデータを処理する必要がある JEE 上のAEM Formsプロセスの XML プロパティファイルを指定します。 デフォルト値は **dataxml** です。

   * **添付ファイルパラメーターの名前** （オプション）:JEE 上のAEM Formsプロセスで処理する必要があるドキュメントオブジェクトのリストを指定します。 デフォルト値は **fileAttachmentsList** です。

1. 設定を確認し、「**保存**」をクリックします。

![Guide LiveCycle Process Locator and Invoker](assets/test3.jpg)

設定が完了すると、「フォームワークフローへの送信」送信アクションには、指定した XML データパラメーターを含む JEE 上の AEM Forms サーバープロセスが一覧表示されます。
