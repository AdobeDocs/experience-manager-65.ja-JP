---
title: 一括アセット移行用の機能パック18912のインストール
description: 機能パック18912では、FTP を使用してアセットを一括で取り込むか、Dynamic Media ClassicからAdobe Experience ManagerのDynamic Mediaにアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 11%

---

# 一括アセット移行用の機能パック18912のインストール{#installing-feature-pack-for-bulk-asset-migration}

機能パック18912のインストールは *オプション* です。

機能パック18912では、FTP を使用して、Dynamic Media - Scene7モードのAdobe Experience Managerに直接アセットを一括取り込むことができます。 また、Experience Manager時に、Dynamic Media ClassicからDynamic Media - Scene7モードにアセットを移行することもできます。 この機能パックは [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) から入手できます。

>[!IMPORTANT]
>
>機能パックを使用して、Dynamic Media ClassicからDynamic Media - Scene7モードにExperience Managerして、自分でアセットを一括移行できます。 また、Dynamic Media Classicの FTP 機能を使用して、アセットを一括移行することもできます。 ただし、Adobeでは *使用しない* これらの方法は、複雑さが原因で使用することをお勧めします。
>
>そのため、この移行機能パックは、[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) を介して行われた場合、移行プロジェクトの一部として *のみ* サポートされます。

機能パックをインストールする前に、サービスユーザーを作成し、その情報をAdobe・サポートに提供します。

[Dynamic Media - Scene7モードの設定 ](/help/assets/config-dms7.md) も参照してください。

**一括アセット移行用の機能パック18912をインストールするには：**

1. Experience Managerインスタンスで、**[!UICONTROL ツール]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL ユーザー]** に移動し、「**[!UICONTROL ユーザーを作成]**」を選択します。 このサービスユーザーは、*読み取り/書き込み* 権限を `/content/dam.` に付与する必要があります
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。アセットが FTP からアップロードされると、FTP サーバーにアップロードされたアセットが作成されたと見なされ、Experience Managerにプッシュされます。
1. [Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) のAdobeカスタマーサポートに連絡して、機能パック18912へのアクセス権をリクエストしてダウンロードしてください。 サポートに問い合わせる際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバー IP アドレス（ポート番号を含む）（デフォルトでは、ポート番号は 4502）。
   * Experience Manager・サービスのユーザー名とパスワードは、前の手順で作成しました。

1. AdobeカスタマーサポートのExperience Managerでは、FTP の資格情報と機能パック18912へのアクセス権が提供されます。
1. 機能パック18912を受け取ったら、インストールします。

   Experience Managerでのソフトウェア配布とパッケージの使用について詳しくは、[ パッケージの使い方 ](/help/sites-administering/package-manager.md) を参照してください。
