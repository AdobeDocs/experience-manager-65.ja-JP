---
title: 多言語アセットとアセット翻訳
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に変換するワークフローの自動化方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 40%

---


# 多言語のアセット {#multilingual-assets}

[!DNL Adobe Experience Manager Assets] を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

To automate translation workflows, you integrate translation service providers with [!DNL Experience Manager] and create projects for translating assets into multiple languages. [!DNL Experience Manager] では人間による翻訳と機械翻訳のワークフローがサポートされます。

Human translation: The translated assets are returned and imported into [!DNL Experience Manager]. When your translation provider is integrated with [!DNL Experience Manager], assets are automatically sent between [!DNL Experience Manager] and the translation provider.

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [Experience Managerと翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

If your translation service provider does not provide a connector to integrate with [!DNL Experience Manager], use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Create translation projects for content fragments](creating-translation-projects-for-content-fragments.md).
