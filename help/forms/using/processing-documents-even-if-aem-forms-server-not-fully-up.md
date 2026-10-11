---
title: AEM Forms サーバーは、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。
description: AEM Forms サーバーは、JEE サーバーおよび OSGi サーバー上ですべてのサービスが起動して実行される前でも、ドキュメントの処理を開始します。
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
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
source-wordcount: '129'
ht-degree: 100%
---
# AEM Forms サーバーは、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 問題 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

AEM Forms サーバーが完全に起動し、すべてのアプリケーションが起動して実行される前に、AEM Forms サーバーはドキュメントの処理を開始します。


## 適用先 {#applies-to}

このソリューションは、JEE サーバー上の AEM Forms と OSGi サーバー上の AEM Forms に適用されます。

## 解決策 {#solution}

この問題を解決するには、サーバーの起動時に引数 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` を[バッチファイル](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/deploying/command-line-start-and-stop#windows-platform-start-bat-script-example)に追加します。
