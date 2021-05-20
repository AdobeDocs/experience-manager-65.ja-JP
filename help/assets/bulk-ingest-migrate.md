---
title: 一括アセット移行用の機能パック18912をインストールしています
description: 機能パック18912では、FTPを使用してアセットを一括で取り込むか、Dynamic Media ClassicからAEM上のDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: アセット管理
role: Business Practitioner, Administrator
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 21%

---

# 一括アセット移行用の機能パック18912をインストールしています{#installing-feature-pack-for-bulk-asset-migration}

機能パック18912のインストールは&#x200B;*オプション*&#x200B;です。

機能パック18912では、AEM上でFTPを使用してDynamic Media - Scene7モードに直接アセットを一括で取り込むか、AEM上でDynamic Media ClassicからDynamic Media - Scene7モードにアセットを移行できます。 この機能パックは、[Adobe Professional Services](https://www.adobe.com/jp/experience-cloud/consulting-services.html)から入手できます。

>[!NOTE]
>
>機能パックを使用して、Dynamic Media ClassicからDynamic Media - AEMのScene7モードにアセットを一括移行することも、Dynamic Media ClassicのFTP機能を使用してアセットを一括移行することもできますが、複雑さのため、Adobeではこの方法を推奨しません。**
>
>そのため、[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)を介して行われた場合、移行プロジェクトの一部として&#x200B;*のみ*&#x200B;がサポートされます。

機能パックをインストールする前に、まずサービスユーザーを作成し、その情報をAdobeサポートに提供する必要があります。

[Dynamic Media - Scene7モード](/help/assets/config-dms7.md)の設定も参照してください。

**一括アセット移行用の機能パック18912をインストールするには**

1. AEM インスタンスで、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;に移動して、「**[!UICONTROL ユーザーを作成]**」を選択します。このサービスユーザーは、*`/content/dam.`に対する読み取り/書き込み*&#x200B;権限を持っている必要があります
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされる場合、アセットは、FTP サーバーにアップロードされて AEM にプッシュされる際に作成されたと見なされます。
1. [Adobeのエンタープライズカスタマーケアに連絡して、Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support)の機能パック18912へのアクセス権をリクエストし、ダウンロードを依頼します。 サポートに連絡する際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバーIPアドレス（ポート番号を含む）（デフォルトでは、ポート番号は4502）。
   * 前の手順で作成したAEMサービスのユーザー名とパスワード。

1. Adobeエンタープライズカスタマーケア(AEM)は、FTP資格情報と機能パック18912へのアクセスを提供します。
1. 機能パック18912を受け取ったら、インストールします。

   AEMでのソフトウェア配布とパッケージの使用について詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。
