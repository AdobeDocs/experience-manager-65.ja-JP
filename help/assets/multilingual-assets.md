---
title: 多言語のアセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に変換するワークフローの自動化方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 20%

---


# 多言語のアセット {#multilingual-assets}

Adobe Experience Manager Assetsを使用すると、アセット（バイナリ、メタデータおよびタグを含む）の翻訳ワークフローを自動化し、多言語プロジェクトで使用する他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーをExperience Managerに統合し、アセットを複数の言語に翻訳するためのプロジェクトを作成します。 Experience Managerは、人力および機械翻訳のワークフローをサポートしています。

人による翻訳： 翻訳済みのアセットが返され、Experience Managerに読み込まれます。 翻訳プロバイダーがExperience Managerと統合されている場合、アセットはExperience Managerと翻訳プロバイダーの間で自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [Experience Managerと翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Create translation projects for content fragments](creating-translation-projects-for-content-fragments.md).
