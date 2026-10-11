---
title: 一括アセット移行用の機能パック 18912 をインストールする
description: 機能パック 18912 では、FTP 経由でアセットを一括取り込みするか、Dynamic Media Classic から Adobe Experience Manager 上の Dynamic Media にアセットを移行できます。 このオプションの機能パックは、アドビサポートから入手できます。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 100%
---
# 一括アセット移行用の機能パック 18912 をインストールする{#installing-feature-pack-for-bulk-asset-migration}

機能パック 18912 のインストールは&#x200B;*オプション*&#x200B;です。

機能パック 18912 を使用すると、FTP 経由で、Adobe Experience Manager 上の Dynamic Media - Scene7 モードに直接アセットを一括取り込みできます。 また、Experience Manager 上で Dynamic Media Classic から Dynamic Media の Scene7 モードにアセットを移行することもできます。 機能パックは、[Adobe プロフェッショナルサービス](https://business.adobe.com/customers/consulting-services/main.html) から入手できます。

>[!IMPORTANT]
>
>機能パックを使用して、Experience Manager で Dynamic Media Classic から Dynamic Media の Scene7 モードに、自身でアセットを一括移行できます。 Dynamic Media Classic の FTP 機能を使用して、アセットを一括移行することもできます。 ただし、複雑さが伴うため、アドビはこれらの方法のいずれかの使用はお勧め&#x200B;*しません*。
>
>そのため、この移行機能パックは、[Adobe プロフェッショナルサービス](https://business.adobe.com/customers/consulting-services/main.html)を通して行われる移行プロジェクトの一部として&#x200B;*のみ*&#x200B;サポートされます。

機能パックをインストールする前に、サービスユーザーを作成し、その情報をアドビサポートに提供します。

[Dynamic Media の Scene7 モードを設定](/help/assets/config-dms7.md)も参照してください。

**一括アセット移行用の機能パック 18912 をインストールするには：**

1. Experience Manager インスタンスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;に移動して、「**[!UICONTROL ユーザーを作成]**」を選択します。 このサービスのユーザーは、`/content/dam.` に対する&#x200B;*読み取り／書き込み*&#x200B;権限を持っている必要があります。
1. 「**[!UICONTROL ID]**」および「**[!UICONTROL パスワード]**」フィールドで、ユーザー名およびパスワードを入力します（例：**FTP User**）。 この名前は、アセットを作成したユーザーとしてタイムラインに表示されます。 アセットが FTP からアップロードされると、アセットは、FTP サーバーにアップロードされたと見なされ、Experience Manager にプッシュされます。
1. [Experience Manager のアドビカスタマーサポート](https://experienceleague.adobe.com/?support-solution=General&lang=ja#support)に連絡して、機能パック 18912 のダウンロードのためのアクセス権をリクエストしてください。 サポートに連絡する際には、次の情報が必要になる場合があります。

   * オーサーインスタンスのサーバー IP アドレスとポート番号（デフォルトのポート番号は 4502）。
   * 前の手順の Experience Manager サービスユーザーのユーザー名とパスワード。

1. Experience Manager のアドビカスタマーサポートは、FTP 資格情報と機能パック 18912 へのアクセス権を提供します。
1. 機能パック 18912 を受け取ったら、インストールします。

   ソフトウエア配布と Experience Manager のパッケージの使用について詳しくは、[パッケージの操作方法](/help/sites-administering/package-manager.md)を参照してください。
