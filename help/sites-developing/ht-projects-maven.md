---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
translation-type: tm+mt
source-git-commit: 7bbafbd96ec92ed4278f6fa1d9899a3d59ee69ad
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 32%

---


# Apache Maven を使用して AEM プロジェクトをビルドする方法 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5は、オンプレミスとAMSの両方の実装の最新のAEM Project Archetypeによって実装された、パッケージ管理とプロジェクト構造の最新のベストプラクティスに従います。

>[!TIP]
>
>詳しくは、次を参照してください。
>
>* AEMの [AEM Project Structure](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) （プロジェクト構造）記事は、最新のAEMプロジェクトの構造を作成する方法に関するCloud Serviceドキュメントとして提供されています。
>* アーキタイプを使用して新しいAEMプロジェクトを開始する方法については、 [AEMプロジェクトのアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html) ・ドキュメントを参照してください。
>* AEMの「 [AdobeコンテンツパッケージMavenプラグイン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=en#developer-tools) 」の記事は、AEMアプリケーションの展開方法に関するCloud Serviceドキュメントとして提供されています。

>
>
3つのドキュメントはすべてAEM 6.5に適用されます。
