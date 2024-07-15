---
title: ここでは、CRX パッケージマネージャーを使用してForms アドオンパッケージをアンインストールする手順を説明します。
description: CRX パッケージマネージャーを使用してForms アドオンパッケージをアンインストールする手順について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# AEM インスタンスからAEM Forms アドオンパッケージをアンインストールする

この記事では、AEM Forms SDK インスタンスからAEM Forms アドオンパッケージを適切にアンインストールするために必要な手順の概要を説明します。 次の手順に従って、Forms アドオンパッケージを確実に削除し、AEM環境で発生する可能性のある問題を防ぎます。

## 前提条件

データの損失を避けるために、必ずバックアップを取ります。

## AEM Forms アドオンパッケージをアンインストールするには

AEM Forms アドオンパッケージをアンインストールするには、次の手順を実行します。

1. **AEM Forms アドオンパッケージをアンインストールします。**
   1. `http://[host]:[port]/crx/de/index.jsp` に移動します。
   1. `AEM Forms add-on package` を探してアンインストールします。

   ![ パッケージをアンインストール ](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **CRXDE からネイティブフォルダーを削除します：**
   1. `http://[host]:[port]/crx/de/index.jsp` に移動します。
   1. `/libs/fd/native/install` に移動して、CRXDE でフォルダー `native` 削除します。

      ![CRX/de からネイティブノードを削除 ](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 変更を保存します。

1. **AEM Forms SDK を停止します。**
   1. 「Ctrl + C」コマンドを使用して、AEM Forms SDK インスタンスを停止します。

1. **岩盤を確認し、crx-quickstart フォルダーにフォルダーをインストールする**
   1. AEM Forms SDK インスタンス `..author\crx-quickstart` フォルダーに移動します。
   1. `bedrock` および `install` という名前のフォルダーを検索します。
見つかった場合は、AEM Forms SDK インスタンスの `crx-quickstart` フォルダーから削除されていることを確認します。

   >[!NOTE]
   >
   > AEM Forms SDK インスタンスを再起動すると、`bedrock` フォルダーが自動的に再作成されます。

1. **AEM インスタンスを再起動します。**
   1. ここまでのすべての手順が完了したら、[AEM Forms SDK インスタンスを再起動 ](/help/forms/using/restart-aem-sdk.md) します。




