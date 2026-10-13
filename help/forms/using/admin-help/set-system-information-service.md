---
title: システム情報サービスのセットアップ
description: システム情報サービスの設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 734ed463-2441-49fc-bacb-deb40851af42
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
source-wordcount: '114'
ht-degree: 100%
---
# システム情報サービスのセットアップ {#set-up-the-system-information-service}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

システム情報サービスは情報取得のために REST API を提供します。 システム情報サービスを使用するには、管理コンソールから REST エンドポイントを有効にします。 REST エンドポイントを有効にするには、次の手順を実行します。

1. 管理コンソールにログインします。 管理コンソールのデフォルト URL は `https://[hostname]:'port'/adminui.` です。
1. サービス／アプリケーションおよびサービス／サービスの管理に移動します。
1. サービス管理ページで、「**SystemInfo**」サービスをクリックします。
1. 「エンドポイント」タブのリストで、「REST」を選択して、「**追加**」をクリックします。
1. REST エンドポイント画面で、「**追加**」をクリックします。
