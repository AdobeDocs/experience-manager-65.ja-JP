---
title: フォームの操作
description: AEM Forms アプリケーションでタスクまたはスタートポイントに関連付けられているフォームを表示および更新する
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 96%
---
# フォームの操作 {#working-with-a-form}

>[!NOTE]
>
>AEM Forms アプリは現在、非推奨です。 質問またはヘルプについては、[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)までお問い合わせください。

Forms アプリケーションでフォームの同期が有効になっている場合、フォームをダウンロードしてアプリ内で直接操作できます。

フォームをアプリにダウンロードして、オフラインで使用することができます。 例えば、金融関係の会社を経営していて、顧客がサイト上で申込書を記入するとします。 アプリケーションは顧客からの情報を受け取り、レビュー用に保存するアダプティブフォームです。 管理者はフォームをレビューし、AEM オーサーインスタンスで検証フォームを作成します。 管理者は、フォームと AEM Forms アプリの同期を有効にします。 検証フォームが AEM Forms アプリケーションで使用できる場合、フィールドエージェントはモバイルデバイスを使用して顧客の詳細を確認できます。 モバイルデバイスはサーバーと同期し、検証フォームがアプリに読み込まれます。 フィールドエージェントは顧客を訪問し、詳細を検証した上で、データをドラフトとして保存するか、検証フォームを送信します。 アプリがオンラインになるたびに、フォームはサーバーと同期されます。

AEM Forms アプリケーションでは、次のようにフォームを同期します。

1. オーサーインスタンスでは、フォームを選択し、**「プロパティの表示」**&#x200B;をクリックします。
1. プロパティページで、**詳細**&#x200B;をクリックします。
1. 詳細で「**AEM Forms アプリと同期**」オプションを有効にし、「**保存**」を選択します。

複数のフォームを同期するには、オーサーインスタンスで、フォームマネージャーから複数のフォームを選択して、「**AEM Forms アプリと同期**」を選択します。 フォームが公開されると、AEM Forms アプリはパブリッシュサーバーに接続してフォームを取得することができます。

AFA（AEM Form Application）Android アプリの同期に失敗した場合は、次の手順を実行して同期の問題を修正します。

1. **https://[server]:[port]/system/console/configMgr** に移動します。
1. **[!UICONTROL Adobe Granite トークン認証ハンドラー]**&#x200B;を検索し、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL SameSite 属性の login-token Cookie]** のドロップダウンメニューから、オプション「**[!UICONTROL なし]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックします。

![AFA Android アプリと画像を同期](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>以下のフォームがサポートされています。
>
>* アダプティブフォーム（遅延読み込みなし）
>* モバイルフォーム
>
>フォームレベルの添付ファイルは、AEM Forms OSGi サーバーと同期している AEM Forms アプリケーションで取得されたアダプティブフォームではサポートされていません。 フォームの作成時に作成者がフィールドレベルの添付ファイルを有効にしている場合は、フィールドにファイルを添付することができます。


**フォームを開いて更新するには**

1. フォームを開くには、ホーム画面に表示されている「**[!UICONTROL フォーム]**」を選択します。
1. フォームのフィールドの更新、添付ファイルの追加、ドラフトとして保存、送信の操作を行うことができます。
