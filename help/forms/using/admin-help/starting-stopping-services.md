---
title: サービスの開始と停止
description: AEM Formsモジュールと、アプリケーションサーバーおよびデータベースに関連するサービスを開始および停止する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 21%

---

# サービスの開始と停止 {#starting-and-stopping-services}

AEM forms には、次の 2 種類のサービスが含まれます。

* AEM forms アプリケーションサーバーとデータベースを制御するサービス。
* AEM forms モジュールを制御するサービス

## AEM forms モジュールに関連付けられたサービスを開始または停止します {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM forms モジュール (Forms、Rights Management、出力など ) は、サービスとして動作します。 これらのAEM forms モジュールのサービスは、場合によっては停止または開始する必要があります。 例えば、サービスの設定を変更した後、AEM forms サービスを停止してから再起動する必要があります。

1. 管理コンソールで、**サービス**／**アプリケーションおよびサービス**／**サービスの管理**&#x200B;をクリックしてください。
1. 「サービスの管理」ページで、停止または開始するサービスの横にあるチェックボックスを選択し、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスを開始または停止します {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、アプリケーションサーバーとデータベースサービスが含まれます。

* AEM Forms 用の *`[application server]`*
* AEM Forms 用の *`[database]`*

Windows では、これらのサービスには、**管理ツール**／**サービスパネル**&#x200B;からアクセスできます。例えば、自動オプションを使用して JBoss にAEM forms をインストールした場合、システム上で次のサービスを使用できます。

* JBoss for Adobe Experience Manager forms
* Adobe Experience Manager forms の MySQL

サービスパネルのリストからサービスを選択し、パネルの適切なアクションボタンをクリックして、これらのサービスを開始または停止します。

UNIX® または Linux では、コマンドラインから次のテキストを入力します。*`[service name]`* には、確認するサービスの名前を指定します。

```java
     ps -A | grep [service name]
```
