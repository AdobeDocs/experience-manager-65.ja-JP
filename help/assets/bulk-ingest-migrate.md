---
title: 一括アセット移行用の機能パック18912のインストール
description: 機能パック18912では、FTPを使用してアセットを一括で取り込むか、Dynamic Media ClassicからAdobe Experience ManagerのDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: アセット管理
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 12%

---

# 一括アセット移行用の機能パック18912のインストール{#installing-feature-pack-for-bulk-asset-migration}

機能パック18912のインストールは&#x200B;*オプション*&#x200B;です。

機能パック18912では、FTPを使用して、Dynamic Media - Scene7モード(Adobe Experience Manager上)に直接アセットを一括で取り込むことができます。 また、Experience Manager時に、Dynamic Media ClassicからDynamic Media - Scene7モードにアセットを移行することもできます。 この機能パックは、[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)から入手できます。

>[!IMPORTANT]
>
>機能パックを使用して、独自のアセットをDynamic Media ClassicからDynamic Media - Scene7モードにExperience Managerで一括移行できます。 また、Dynamic Media ClassicのFTP機能を使用して、アセットを一括移行することもできます。 ただし、Adobeは複雑なので、*使用しない*&#x200B;をお勧めします。
>
>そのため、この移行機能パックは、[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)を介して行われた場合、移行プロジェクトの一部として&#x200B;*のみ*&#x200B;サポートされます。

機能パックをインストールする前に、サービスユーザーを作成し、その情報をAdobe・サポートに提供します。

[Dynamic Media - Scene7モード](/help/assets/config-dms7.md)の設定も参照してください。

**一括アセット移行用の機能パック18912をインストールするには：**

1. Experience Managerインスタンスで、**[!UICONTROL ツール]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL ユーザー]**&#x200B;に移動し、「**[!UICONTROL ユーザーを作成]**」を選択します。 このサービスユーザーは、*`/content/dam.`に対する読み取り/書き込み*&#x200B;権限を持っている必要があります
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。FTPからアセットがアップロードされると、FTPサーバーにアップロードされてExperience Managerにプッシュされたと見なされます。
1. [Adobeのエンタープライズカスタマーケアに連絡して、Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support)の機能パック18912へのアクセス権をリクエストし、ダウンロードを依頼します。 サポートに連絡する際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバーIPアドレス（ポート番号を含む）（デフォルトでは、ポート番号は4502）。
   * 前の手順で作成したExperience Manager・サービスのユーザー名とパスワード。

1. AdobeエンタープライズカスタマーケアExperience Managerは、FTP資格情報と機能パック18912へのアクセス権を提供します。
1. 機能パック18912を受け取ったら、インストールします。

   Experience Managerでのソフトウェア配布とパッケージの使用について詳しくは、[パッケージの使い方](/help/sites-administering/package-manager.md)を参照してください。
