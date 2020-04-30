---
title: 一括アセット移行のための機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括インジェストするか、AEM上のDynamic Media Classicからダイナミックメディアにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Installing feature pack 18912 for bulk asset migration{#installing-feature-pack-for-bulk-asset-migration}

The installation of feature pack 18912 is *optional*.

機能パック18912では、FTP経由でアセットを直接ダイナミックメディア — Scene7モードに一括インジェストするか、AEMでアセットをダイナミックメディアクラシックからダイナミックメディア — Scene7モードに移行できます。 この機能パックは、 [Adobe Professional Servicesから入手できます](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>機能パックを使用して、AEMのDynamic Media ClassicからDynamic Media - Scene 7モードにアセットを一括移行したり、Dynamic Media ClassicのFTP機能を使用してアセットを一括移行したりできますが、複雑さのため ** 、この方法はお勧めしません。
>
>したがって、このような移行機能パックは *、* Adobe Professional Servicesを通じて行う場合にのみ、移行プロジェクトの一部としてサポートさ [れます](https://www.adobe.com/jp/experience-cloud/consulting-services.html)。

機能パックをインストールする前に、まずサービスユーザーを作成し、その情報をアドビのサポートに提供する必要があります。

See also [Configuring Dynamic Media - Scene7 mode](/help/assets/config-dms7.md).

**一括アセット移行用の機能パック18912をインストールするには**

1. AEM インスタンスで、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;に移動して、「**[!UICONTROL ユーザーを作成]**」を選択します。This service user must have *read/write* permissions to `/content/dam.`
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. Experience Managerのアドビエ [ンタープライズカスタマーケアに問い合わせて](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) 、機能パック18912のダウンロードをリクエストします。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * 作成者インスタンスのサーバーIPアドレス。ポート番号を含みます（デフォルトでは、ポート番号は4502です）。
   * 前の手順のAEMサービスのユーザー名とパスワード。

1. AEMのアドビエンタープライズカスタマーケアでは、FTPの資格情報と機能パック18912へのアクセスを提供しています。
1. 機能パック18912を受け取ったら、インストールします。

   See [How to Work with Packages](/help/sites-administering/package-manager.md) for more information on using Package Share and packages in AEM.
