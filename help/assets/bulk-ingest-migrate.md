---
title: 一括アセット移行のための機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEMのDynamic MediaクラシックからDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 21%

---


# 一括アセット移行用の機能パック18912をインストールしています{#installing-feature-pack-for-bulk-asset-migration}

機能パック18912のインストールは&#x200B;*オプション*&#x200B;です。

機能パック18912では、FTP経由でアセットを直接Dynamic Media-Scene7モードにバルクインジェストするか、アセットをAEM上でDynamic MediaクラシックからDynamic Media-Scene7モードに移行できます。 この機能パックは[Adobe Professional Services](https://www.adobe.com/jp/experience-cloud/consulting-services.html)から入手できます。

>[!NOTE]
>
>機能パックを使用して、AEMのDynamic MediaクラシックからDynamic Media- Scene7モードにアセットを一括移行したり、Dynamic MediaクラシックのFTP機能を使用してアセットを一括移行することは可能ですが、Adobeは複雑さのため、この方法を推奨しません。**
>
>したがって、[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)を介して行われた場合、移行プロジェクトの一部として&#x200B;**&#x200B;のみがサポートされます。

機能パックをインストールする前に、サービスユーザーを作成し、その情報をAdobeサポートに提供する必要があります。

[Dynamic Mediaの設定 —Scene7モード](/help/assets/config-dms7.md)も参照してください。

**一括アセット移行用の機能パック18912をインストールするには**

1. AEM インスタンスで、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;に移動して、「**[!UICONTROL ユーザーを作成]**」を選択します。このサービスユーザーは、`/content/dam.`に対する&#x200B;*読み取り/書き込み*&#x200B;権限が必要です
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. 機能パック18912のダウンロードをリクエストするには、[AdobeエンタープライズカスタマーケアにExperience Manager](https://experienceleague.adobe.com/?support-solution=General#support)にお問い合わせください。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号（デフォルトでは、ポート番号は4502）を含みます。
   * 前の手順のAEMサービスユーザー名とパスワード。

1. Adobeエンタープライズカスタマーケア(AEM)では、FTP資格情報と機能パック18912へのアクセス権が提供されます。
1. 機能パック18912を受け取ったら、インストールします。

   AEMでのソフトウェア配布とパッケージの使用方法の詳細については、[How to Work with Packages](/help/sites-administering/package-manager.md)を参照してください。
