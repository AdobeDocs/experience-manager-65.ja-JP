---
title: AEM Formsが開始していないにもかかわらず、複数のサービスの実行。
description: AEM Formsが完全に起動していなくても、複数のサービスを処理します。
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# AEM Formsが完全に開始していないにもかかわらず、複数のサービスの実行{#steps-to-resolve-error-after-installing-service-pack}


## イシュー {#issue}

ユーザーがAEM Formsを再起動しても、現在の呼び出しプロセス (PDFドキュメントのレンダリングなど ) は続行されます。 これにより、AEM Formsサーバーが正しく再起動しません。

## 適用先 {#applies-to}

このソリューションは、JEE 上のAEM Forms Server と OSGi 上のAEM Formsに適用されます。

## ソリューション {#solution}

この問題を解決するには、ユーザーは引数を追加します `Dcom.adobe.livecycle.dsc.deferServiceStart=true` から [バッチファイル](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) サーバの起動中に





