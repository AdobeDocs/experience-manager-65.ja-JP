---
title: メンテナンスモードでの AEM Forms の実行
description: メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行するときに役立ちます。メンテナンスモードでの AEM Forms の実行について詳しく学びます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# メンテナンスモードでの AEM Forms の実行 {#running-aem-forms-in-maintenance-mode}

メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行するときに役立ちます。

サーバーがメンテナンスモードのときはプロセスを一切開始しないでください。サーバーがメンテナンスモードのときにプロセスを開始すると、次の問題が発生します。

* プロセスの有効期間が長い場合、プロセスはジョブデータベースに追加されますが開始されません。メンテナンスモードを終了すると、メンテナンスモード中にサーバーが再起動した場合でも、キューにある長期間有効なジョブが AEM Forms で処理されます。
* プロセスの有効期間が短い場合はすぐに処理されます。

**AEM Forms をメンテナンスモードにする**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   ブラウザーウィンドウに「一時停止中」のメッセージが表示されます。

   >[!NOTE]
   >
   >メンテナンスモードの間にサーバーをシャットダウンすると、再起動してもメンテナンスモードのままです。メンテナンスタスクを終了したら、メンテナンスモードをオフにします。

**AEM Forms がメンテナンスモードで実行中かどうかの確認**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   ブラウザーウィンドウにステータスが表示されます。「true」のステータスはサーバーがメンテナンスモードで動作中であることを示し、「false」はサーバーがメンテナンスモードではないことを示します。

**メンテナンスモードをオフにする**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   ブラウザーウィンドウに「実行中」のメッセージが表示されます。
