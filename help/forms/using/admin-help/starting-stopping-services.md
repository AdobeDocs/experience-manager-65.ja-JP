---
title: サービスの開始と停止
seo-title: サービスの開始と停止
description: AEM Forms モジュール、アプリケーションサーバー、データベースに関連付けられたサービスを開始および停止する方法について説明します。
seo-description: AEM Forms モジュール、アプリケーションサーバー、データベースに関連付けられたサービスを開始および停止する方法について説明します。
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 82%

---


# サービスの開始と停止 {#starting-and-stopping-services}

AEM Forms に含まれるサービスには以下の 2 種類があります。

* AEM Forms アプリケーションサーバーおよびデータベースを制御するサービス
* AEM Forms モジュールを制御するサービス

## AEM Forms モジュール関連サービスの開始と停止 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Forms モジュール（例えば、Forms、Rights Management、Output）がサービスとして動作します。これらの AEM Forms モジュールのサービスは、場合によって起動または停止する必要があります。例えば、サービスの設定を変更した後には、AEM Forms サービスを停止してから再起動する必要があります。

1. In administration console click **Services** > **Applications and Services** > **Service Management**.
1. サービスの管理ページで、停止または開始するサービスの隣のチェックボックスを選択して、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスの開始と停止 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、以下のアプリケーションサーバーおよびデータベースのサービスが含まれています。

* *`[application server]`* （AEM Formsの場合）
* *`[database]`* （AEM Formsの場合）

On Windows, these services are accessible through the **Administrative Tools** > **Services panel**. 例えば、自動オプションを使用して JBoss に AEM Forms をインストールした場合、システムでは以下のサービスを使用できます。

* JBoss for Adobe Experience Manager forms
* MySQL for Adobe Experience Manager forms

これらのサービスを開始または停止するには、リストからサービスを選択し、パネルの適切なアクションボタンをクリックします。

On UNIX® or Linux, enter the following text from a command line, where *`[service name]`* is the name of the service you are verifying:

```java
     ps -A | grep [service name]
```

