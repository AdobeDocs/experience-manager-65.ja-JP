---
title: Geometrixx サイトの削除
description: サンプルの Geometrixx コンテンツの削除方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: ht
source-wordcount: '126'
ht-degree: 100%

---


# Geometrixx サイトの削除{#removing-the-geometrixx-sites}

AEM には一連の Geometrixx サンプル web サイトが付属しています。このサンプルコンテンツを&#x200B;**パッケージマネージャー**&#x200B;経由で削除できます。

geometrixx 関連の個別のパッケージは次のとおりです。

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

個別のパッケージを削除するには、そのパッケージで「**アンインストール**」をクリックします。

また、以下のスーパーパッケージがあります。

* `cq-geometrixx-all-pkg-5.6.12.zip`

このパッケージには、上記の個々のパッケージがすべて含まれています。すべての geometrixx 関連のコンテンツを一度に削除するには、このパッケージの「**アンインストール**」をクリックします。スーパーパッケージが未インストールの状態になり、個々のパッケージはすべて、パッケージマネージャーに表示されなくなります。

これで、デモンストレーションサイトが含まれない「空の」AEM インスタンスが作成されます。

>[!NOTE]
>
>アップグレードの際には、Geometrixx サイトが自動的に再作成されます。これらのサンプルが不要な場合は、アップグレード後に Geometrixx web サイトを削除します。

