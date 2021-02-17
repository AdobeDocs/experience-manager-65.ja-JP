---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
translation-type: tm+mt
source-git-commit: 7bbafbd96ec92ed4278f6fa1d9899a3d59ee69ad
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 49%

---


# Apache Maven を使用して AEM プロジェクトをビルドする方法 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5 は、オンプレミス実装と AMS 実装の最新の AEM プロジェクトアーキタイプで実装されているパッケージ管理とプロジェクト構造の最新のベストプラクティスに従っています。

>[!TIP]
>
>詳しくは、次を参照してください。
>
>* AEMの[AEM Project Structure](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)記事は、最新のAEMプロジェクトの構造化方法に関するCloud Serviceドキュメントとして提供されています。
>* アーキタイプを使用して新しいAEMプロジェクトを開始する方法については、[AEMプロジェクトのアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)のドキュメントを参照してください。
>* AEMの[AdobeコンテンツパッケージMavenプラグイン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=en#developer-tools)の記事は、AEMアプリケーションの展開方法に関するCloud Serviceドキュメントとして提供されています。

>
>
3つのドキュメントはすべてAEM 6.5に適用されます。
