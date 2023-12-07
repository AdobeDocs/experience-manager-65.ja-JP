---
title: メンテナンスモードでの AEM Forms の実行
description: メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行する場合に役立ちます。 メンテナンスモードでのAEM forms の実行に関する詳細
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 8%

---

# メンテナンスモードでの AEM Forms の実行 {#running-aem-forms-in-maintenance-mode}

メンテナンスモードは、DSC のパッチ適用、AEM Forms のアップグレード、サービスパックの適用などのタスクを実行する場合に役立ちます。

サーバーがメンテナンスモードの間は、プロセスを呼び出さないでください。 サーバーがメンテナンスモードの間にプロセスが呼び出された場合は、次のようになります。

* プロセスが長期間有効な場合、ジョブデータベースに追加されますが、開始されません。 メンテナンスモードを終了すると、メンテナンスモード中にサーバーを再起動した場合でも、AEM forms はキュー内の長期間有効なジョブを処理します。
* プロセスの有効期間が短い場合は、すぐに処理されます。

**AEM forms をメンテナンスモードにする**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   ブラウザーウィンドウに「一時停止中」のメッセージが表示されます。

   >[!NOTE]
   >
   >メンテナンスモードの間にサーバーをシャットダウンした場合、サーバーを再起動してもメンテナンスモードのままです。 メンテナンスタスクが終了したら、メンテナンスモードをオフにします。

**AEM forms がメンテナンスモードで実行されているかどうかの確認**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   ブラウザーウィンドウにステータスが表示されます。 ステータスが「true」の場合は、サーバーがメンテナンスモードで実行されていることを示し、「false」の場合は、サーバーがメンテナンスモードではありません。

**メンテナンスモードをオフにする**

1. Web ブラウザーに次のように入力します。

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   ブラウザーウィンドウに「実行中」のメッセージが表示されます。
