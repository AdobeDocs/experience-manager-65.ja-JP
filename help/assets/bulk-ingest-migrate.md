---
title: 一括アセット移行のための機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括取り込むか、アセットをAEM上のダイナミックメディアに移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 22%

---


# Installing feature pack 18912 for bulk asset migration{#installing-feature-pack-for-bulk-asset-migration}

The installation of feature pack 18912 is *optional*.

機能パック18912では、FTP経由でアセットを直接ダイナミックメディア —Scene7モードにバルクインジェストするか、AEMでアセットをダイナミックメディア —Scene7モードに移行できます。 機能パックは [Adobe Professional Servicesから入手できます](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>機能パックを使用して、AEMのDynamic Media ClassicからDynamic Media Scene 7モードにアセットを一括移行したり、Dynamic Media ClassicのFTP機能を使用してアセットを一括移行したりすることは可能ですが ** 、Adobeは複雑なためこの方法を推奨しません。
>
>したがって、このような移行機能パックは、 *Adobe Professional Services経由で行う場合の移行プロジェクトの一部としての* みサポートされます [](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

機能パックをインストールする前に、サービスユーザーを作成し、その情報をAdobeサポートに提供する必要があります。

See also [Configuring Dynamic Media - Scene7 mode](/help/assets/config-dms7.md).

**一括アセット移行用の機能パック18912をインストールするには**

1. AEM インスタンスで、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;に移動して、「**[!UICONTROL ユーザーを作成]**」を選択します。This service user must have *read/write* permissions to `/content/dam.`
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. 機能パック18912のダウンロードをリクエストするには、 [AdobeエンタープライズカスタマーケアにExperience Managerを依頼してください](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) 。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号（デフォルトでは、ポート番号は4502）を含みます。
   * 前の手順のAEMサービスユーザー名とパスワード。

1. Adobeエンタープライズカスタマーケア(AEM)では、FTP資格情報と機能パック18912へのアクセス権が提供されます。
1. 機能パック18912を受け取ったら、インストールします。

   See [How to Work with Packages](/help/sites-administering/package-manager.md) for more information on using Software Distribution and packages in AEM.
