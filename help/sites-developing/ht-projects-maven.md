---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 49%

---

# Apache Maven を使用して AEM プロジェクトをビルドする方法 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5 は、オンプレミス実装と AMS 実装の最新の AEM プロジェクトアーキタイプで実装されているパッケージ管理とプロジェクト構造の最新のベストプラクティスに従っています。

>[!TIP]
>
>詳しくは、以下を参照してください。
>
>* AEMの最新のAEMプロジェクトの構造に関するCloud ServiceドキュメントとしてのAEMプロジェクト構造の[記事。](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
>* アーキタイプを使用して新しいAEMプロジェクトを開始する方法については、 [AEMプロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)のドキュメントを参照してください。
>* AEMアプリケーションのデプロイ方法に関するCloud ServiceドキュメントとしてのAEMの[AdobeコンテンツパッケージMaven Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=en#developer-tools)に関する記事。

>
>
3つのドキュメントはすべてAEM 6.5に適用されます。
