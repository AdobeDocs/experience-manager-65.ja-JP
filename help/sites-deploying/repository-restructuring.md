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
feature: アップグレード
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 61%

---

# AEM 6.5 におけるリポジトリの再構築{#repository-restructuring-in-aem}

## はじめに {#introduction}

AEM 6.4より前は、顧客コードは、JCRの予測できない領域にデプロイされ、アップグレード時に変更される可能性がありました。 このため、正式なAEMリリースでは、カスタムコード、設定またはコンテンツが上書きされることがよくありました。 逆に、カスタムのコードや設定やコンテンツが AEM の製品コードやコンテンツを上書きしてしまい、製品の機能が損なわれることもありました。

AEM 製品コードとカスタムコードの階層を明確に記述すれば、このような競合を回避できます。

そのために、AEM 6.4以降のリリースで引き続き、コンテンツは/etcからリポジトリ内の他のフォルダーに再構築され、コンテンツの移動先に関するガイドラインと共に、次の大まかなルールに従っています。

* AEM 製品コードは必ず /libs 下に配置されます。このフォルダーをカスタムコードで上書きしてはなりません。
* カスタムコードは/apps、/contentおよび/confに配置する必要があります。

## 6.5 へのアップグレード時の影響 {#impact-on-upgrades}

AEM 6.5 にアップグレードすると、/etc の下にあるコンテンツの大部分がリポジトリ内の他のフォルダーに複製されます。これらの新しい場所は、コンテンツが優先的に参照される場所になります。ただし、AEM 6.5 にアップグレードしても /etc フォルダー内の以前の場所との下位互換性を保つことができるようにあらゆる試みがおこなわれてきた結果、ほとんどの場合、顧客のアプリケーションで変更が活発に（多くの場合、手動で）おこなわれるまでは、AEM コードで古い場所が引き続き参照されます。スケジュールの観点からは、変更は次の 2 つのカテゴリに分かれます。

* 6.5 へのアップグレード時におこなう変更 - /etc 再構築に伴う一部の変更は下位互換性がないので、AEM 6.5 へのアップグレードの一環として変更を計画し実行してください。
* 将来のアップグレードの前 — /etc再構築の変更の大部分は、アップグレード後のしばらくの間延期できます。 既に述べたように、顧客へのリリースの一環として変更が実行されるまで、AEM 6.5 コードでは古い場所を引き続き参照します。変更を加える必須のタイムラインはありませんが、将来の機能では参照される新しい場所に依存する可能性があるので、将来のアップグレードの前にタイムラインを作成することをお勧めします。 また、所定の機能のドキュメントは、慣例的に新しい場所を参照することになるので、古い場所がまだ使用されていると、混乱が生じるおそれがあります。

### 再構築ガイダンス{#restructuring-guidance}

AEM 6.5 へのアップグレードを計画している場合は、作業量を評価するために以下のソリューションごとのページを参照してください。

* [すべての AEM ソリューションに共通のリポジトリ再構築](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites のリポジトリ再構築](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assetsのリポジトリ再構築](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media のリポジトリ再構築](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Formsのリポジトリ再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communitiesのリポジトリ再構築](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce のリポジトリ再構築](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

各ページは、必要な変更の緊急度に応じて 2 つの節に分かれます。「6.5 へのアップグレード時におこなう変更」で説明している作業はすべて、AEM 6.5 へのアップグレードプロジェクトの一環として取り組んでください。「今後のアップグレードの前」にある項目は、アップグレード後まで延期することもできます。

ページの各エントリには、新しい場所が以前/etcフォルダーの下にあるコンテンツに対して参照されるように、新しい6.5リポジトリモデルに合わせるための推奨される技術的戦略の詳細を示す「再構築のガイダンス」フィールドが含まれます。 追加の「メモ」フィールドには、有用な関連情報が記載されています。
