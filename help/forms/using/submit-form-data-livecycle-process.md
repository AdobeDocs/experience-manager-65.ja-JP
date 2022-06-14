---
title: AEM Forms がフォームデータを JEE 上の AEM Forms プロセスに送信するための設定
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms を使用すると、アダプティブフォームを JEE 上の AEM Forms プロセスと統合し、フォームデータを処理することができます。
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%

---

# AEM Forms がフォームデータを JEE 上の AEM Forms プロセスに送信するための設定{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

アダプティブフォームは、JEE 上の AEM Forms プロセスへのデータの送信をサポートしているため、データの追加処理を行えます。送信済みフォームの使用可能なデータを使用して JEE 上の AEM Forms プロセスをトリガーできます。次の手順を実行して、AEM Forms インスタンスがアダプティブフォームを AEM Forms on JEE プロセスに送信できるようにします。

## AEM Forms サーバーの設定 {#configure-your-aem-forms-server}

次の手順を実行して、JEE 上の AEM Forms にデータを送信する AEM Forms サーバーを有効にします。

1. AEM web コンソールの設定ページ（https://[*host*]:[*port*]/system/console/configMgr）に移動します。

1. **Adobe LiveCycle Client SDK Configuration** コンポーネントを見つけてクリックします。
1. クリックして、JEE 上の AEM Forms サーバーの URL、ユーザー名、およびパスワードを編集します。
1. 設定を確認し、「**保存**」をクリックします。

![Adobe LiveCycle Client SDK 設定](assets/clientsdkconfiguration.jpg)

## LiveCycle プロセスのフィールドへのデータのマッピング {#map-data-with-process-fields}

AEM Forms の設定が完了したら、データ XML と添付ファイルを、送信済みフォームから JEE 上の AEM Forms プロセスのフィールドにマッピングします。次の手順を実行します。

1. AEM Web Console Configuration で、**Guide LiveCycle Process Locator and Invoker** 設定をクリックして編集します。
1. 以下のパラメーターを指定します。

   * **データ xml パラメーターの名前**（必須）：送信されたデータを処理する必要がある AEM Forms on JEE プロセスの XML プロパティファイルを指定します。デフォルト値は **dataxml** です。

   * **Name of the file attachments parameter**（オプション）：JEE 上の AEM Forms プロセスで処理する必要のあるドキュメントオブジェクトのリストを指定します。デフォルト値は **fileAttachmentsList** です。

1. 設定を確認し、「**保存**」をクリックします。

![Guide LiveCycle Process Locator and Invoker](assets/test3.jpg)

設定が完了すると、「フォームワークフローへの送信」送信アクションには、指定した XML データパラメーターを含む JEE 上の AEM Forms サーバープロセスが一覧表示されます。
