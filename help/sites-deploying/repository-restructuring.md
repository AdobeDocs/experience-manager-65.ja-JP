---
title: AEM 6.5 におけるリポジトリの再構築
seo-title: AEM 6.5 におけるリポジトリの再構築
description: AEM 6.5 におけるリポジトリ再構築の基礎と基本的な考え方について説明します。
seo-description: AEM 6.5 におけるリポジトリ再構築の基礎と基本的な考え方について説明します。
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 61%

---


# AEM 6.5 におけるリポジトリの再構築{#repository-restructuring-in-aem}

## 概要 {#introduction}

AEM 6.4より前は、アップグレード時に変更されるJCRの予測できない領域に、カスタマーコードがデプロイされていました。 このため、正式なAEMリリースでは、カスタムコード、設定、またはコンテンツを上書きするのが一般的でした。 逆に、カスタムのコードや設定やコンテンツが AEM の製品コードやコンテンツを上書きしてしまい、製品の機能が損なわれることもありました。

AEM 製品コードとカスタムコードの階層を明確に記述すれば、このような競合を回避できます。

そのため、AEM 6.4以降、将来のリリースで引き続き提供される予定ですが、コンテンツはリポジトリ内の他のフォルダに/etcで再構成され、コンテンツの移動先に関するガイドラインと共に、次の高レベルの規則に従っています。

* AEM 製品コードは必ず /libs 下に配置されます。このフォルダーをカスタムコードで上書きしてはなりません。
* カスタムコードは、/apps、/content、および/confに配置する必要があります。

## 6.5 へのアップグレード時の影響 {#impact-on-upgrades}

AEM 6.5 にアップグレードすると、/etc の下にあるコンテンツの大部分がリポジトリ内の他のフォルダーに複製されます。これらの新しい場所は、コンテンツが優先的に参照される場所になります。ただし、AEM 6.5 にアップグレードしても /etc フォルダー内の以前の場所との下位互換性を保つことができるようにあらゆる試みがおこなわれてきた結果、ほとんどの場合、顧客のアプリケーションで変更が活発に（多くの場合、手動で）おこなわれるまでは、AEM コードで古い場所が引き続き参照されます。スケジュールの観点からは、変更は次の 2 つのカテゴリに分かれます。

* 6.5 へのアップグレード時におこなう変更 - /etc 再構築に伴う一部の変更は下位互換性がないので、AEM 6.5 へのアップグレードの一環として変更を計画し実行してください。
* 将来のアップグレードの前 — /etc再構築の変更の大部分は、アップグレード後にしばらくなるまで延期できます。 既に述べたように、顧客へのリリースの一環として変更が実行されるまで、AEM 6.5 コードでは古い場所を引き続き参照します。変更を行う必要のある強制タイムラインはありませんが、将来の機能では、参照される新しい場所に依存する可能性があるので、将来のアップグレードの前にタイムラインを行うことをお勧めします。 また、所定の機能のドキュメントは、慣例的に新しい場所を参照することになるので、古い場所がまだ使用されていると、混乱が生じるおそれがあります。

### Restructuring Guidance {#restructuring-guidance}

AEM 6.5 へのアップグレードを計画している場合は、作業量を評価するために以下のソリューションごとのページを参照してください。

* [すべての AEM ソリューションに共通のリポジトリ再構築](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites のリポジトリ再構築](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assetsリポジトリ再構築](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media のリポジトリ再構築](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Formsリポジトリ再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communitiesリポジトリ再構築](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce のリポジトリ再構築](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

各ページは、必要な変更の緊急度に応じて 2 つの節に分かれます。「6.5 へのアップグレード時におこなう変更」で説明している作業はすべて、AEM 6.5 へのアップグレードプロジェクトの一環として取り組んでください。「将来のアップグレードの前」にあるものは、アップグレード後になるまでオプションで延期できます。

ページの各エントリには「再構築ガイダンス」フィールドが含まれています。このフィールドには、新しい場所が以前/etcフォルダーの下にあったコンテンツ用に参照されるように、新しい6.5リポジトリモデルと連携するための推奨技術的な戦略の詳細が記載されています。 追加の「メモ」フィールドには、有用な関連情報が記載されています。
