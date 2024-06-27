---
title: AEM Forms サーバーは、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。
description: AEM Forms サーバーは、JEE サーバーおよび OSGi サーバー上ですべてのサービスが起動して実行される前でも、ドキュメントの処理を開始します。
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: ht
source-wordcount: '111'
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
