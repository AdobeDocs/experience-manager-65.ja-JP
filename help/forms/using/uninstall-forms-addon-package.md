---
title: この記事では、CRX Package Manager を使用してForms アドオンパッケージをアンインストールする手順について説明します。
description: CRX パッケージマネージャーを使用してForms アドオンパッケージをアンインストールする手順を説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 975f1f580404ea1f2940aec5981f5668dced4b95
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---


# AEM インスタンスからAEM Forms アドオンパッケージをアンインストールする

この記事では、AEM Forms SDK インスタンスからAEM Forms アドオンパッケージを適切にアンインストールするために必要な手順の概要を説明します。 次の手順に従って、Forms アドオンパッケージを確実に削除し、AEM環境の潜在的な問題を防ぎます。

## 前提条件

データの損失を避けるために、フォームとデータのバックアップを必ず作成してください。

## AEM Forms アドオンパッケージをアンインストールするには

AEM Forms アドオンパッケージをアンインストールするには、次の手順を実行します。

1. **AEM Forms アドオンパッケージをアンインストールします。**
   1. に移動します。 `http://[host]:[port]/crx/de/index.jsp`.
   1. を探してアンインストールします。 `AEM Forms add-on package`.

   ![パッケージをアンインストール](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **CRXDE からネイティブフォルダーを削除します。**
   1. に移動します。 `http://[host]:[port]/crx/de/index.jsp`.
   1. に移動 `/libs/fd/native/install` と削除 `native` crxde のフォルダー。

      ![CRX/de からネイティブノードを削除](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 変更を保存します。

1. **AEM Forms SDK を停止します。**
   1. 「Ctrl + C」コマンドを使用して、AEM Forms SDK インスタンスを停止します。

1. **岩盤を確認し、crx-quickstart フォルダーにフォルダーをインストールします。**
   1. に移動します。 `..author\crx-quickstart` AEM Forms SDK インスタンスのフォルダー。
   1. という名前のフォルダーの検索 `bedrock` および `install`.
見つかった場合は、必ず次から削除します `crx-quickstart` AEM Forms SDK インスタンスのフォルダー。

   >[!NOTE]
   >
   > この `bedrock` AEM Forms SDK インスタンスを再起動すると、フォルダーが自動的に再作成されます。

1. **AEM インスタンスを再起動します。**
   1. 前のすべての手順が完了したら、 [AEM Forms SDK インスタンスを再起動します](/help/forms/using/restart-aem-sdk.md).




