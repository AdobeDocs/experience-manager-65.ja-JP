---
title: 多言語アセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に翻訳するワークフローを自動化する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Multilingual assets {#multilingual-assets}

Adobe Experience Manager（AEM）Assets を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、アセットを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

人間による翻訳：翻訳済みアセットが返され、AEM に読み込まれます。翻訳プロバイダーと AEM を連携すると、AEM と翻訳プロバイダーとの間でアセットが自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [AEMと翻訳サービスプロバイダーとの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳用のアセットの準備](preparing-assets-for-translation.md)
1. [翻訳クラウドサービスのフォルダーへの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Create translation projects for content fragments](creating-translation-projects-for-content-fragments.md).
