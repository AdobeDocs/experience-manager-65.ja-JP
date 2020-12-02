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

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーを[!DNL Experience Manager]と統合し、アセットを複数の言語に翻訳するためのプロジェクトを作成します。 [!DNL Experience Manager] では人間による翻訳と機械翻訳のワークフローがサポートされます。

人による翻訳：翻訳済みのアセットが返され、[!DNL Experience Manager]に読み込まれます。 翻訳プロバイダーが[!DNL Experience Manager]と統合されている場合、アセットは[!DNL Experience Manager]と翻訳プロバイダーの間で自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [Experience Managerと翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

翻訳サービスプロバイダーに[!DNL Experience Manager]と統合するコネクタがない場合は、[代替プロセス](/help/sites-administering/tc-manage.md#exporting-a-translation-job)を使用します。

[コンテンツフラグメント用の翻訳プロジェクトを作成する](creating-translation-projects-for-content-fragments.md)も参照してください。
