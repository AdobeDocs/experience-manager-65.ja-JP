---
title: AEM Forms Server は、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。
description: JEE サーバーおよび OSGi サーバー上ですべてのサービスが起動して実行される前でも、AEM Formsサーバーはドキュメントの処理を開始します。
source-git-commit: 6f2b16a51d4ad0f5c199ff41e8abe150c27ecc01
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms Server は、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## イシュー {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

AEM Forms Server が完全に起動し、すべてのアプリケーションが起動して実行される前に、AEM Forms Server はドキュメントの処理を開始します。


## 適用先 {#applies-to}

このソリューションは、JEE 上のAEM Forms Server と OSGi 上のAEM Formsに適用されます。

## ソリューション {#solution}

問題を解決するには、引数を追加します。 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` から [バッチファイル](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) サーバの起動中に