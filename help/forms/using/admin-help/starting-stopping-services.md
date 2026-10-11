---
title: サービスの開始と停止
description: AEM Forms モジュール、アプリケーションサーバー、データベースに関連付けられたサービスを開始および停止する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%
---
# サービスの開始と停止 {#starting-and-stopping-services}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

AEM Forms に含まれるサービスには以下の 2 種類があります。

* AEM Forms アプリケーションサーバーおよびデータベースを制御するサービス
* AEM Forms モジュールを制御するサービス

## AEM Forms モジュール関連サービスの開始と停止 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Forms モジュール（例えば、Forms、Rights Management、Output）がサービスとして動作します。 場合によっては、これらの AEM Forms モジュールのサービスを停止または開始する必要があります。 例えば、サービスの設定を変更した後には、AEM Forms サービスを停止してから再起動する必要があります。

>[!NOTE]
>
> 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. 管理コンソールで、**サービス**／**アプリケーションおよびサービス**／**サービスの管理**&#x200B;をクリックしてください。
1. サービスの管理ページで、停止または開始するサービスの隣のチェックボックスをオンにして、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスの開始と停止 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、以下のアプリケーションサーバーおよびデータベースのサービスが含まれています。

* AEM Forms 用の *`[application server]`*
* AEM Forms 用の *`[database]`*

Windows では、これらのサービスには、**管理ツール**／**サービスパネル**&#x200B;からアクセスできます。 例えば、ターンキー方式を使用して JBoss に AEM Forms をインストールした場合、システムでは以下のサービスを使用できます。

* JBoss for Adobe Experience Manager フォーム
* MySQL for Adobe Experience Manager フォーム

これらのサービスを開始または停止するには、サービスパネルのリストからサービスを選択し、パネルの適切なアクションボタンをクリックします。

UNIX® または Linux では、コマンドラインから次のテキストを入力します。*`[service name]`* には、確認するサービスの名前を指定します。

```java
     ps -A | grep [service name]
```
