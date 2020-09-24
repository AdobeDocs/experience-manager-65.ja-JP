---
title: 互換性パッケージ
seo-title: 互換性パッケージ
description: 互換性パッケージをAEM Forms6.5にインストールすると、AEM Forms6.4以前のバージョンと非推奨のアダプティブフォームのテンプレートおよびページから、Correspondence Managementアセットを使用できます
seo-description: 互換性パッケージを AEM Forms 6.4 にインストールすると、AEM Forms 6.4 および非推奨になったアダプティブォームテンプレートとページから Correspondence Management アセットを使用できます
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 59%

---


# 互換性パッケージ{#compatibility-package}

## 概要 {#overview}

Interactive communication is the default and recommended approach to create customer communications in AEM Forms 6.5. To continue using letters in AEM Forms 6.5, you need to install the latest [AEMFD Compatibility package](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html).

The AEMFD Compatibility package also allows you to [use the following assets from AEM Forms 6.4, 6.3 and 6.2 on AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨になったテンプレートおよびページ

For more information, see [Assets made compatible with AEM Forms 6.5 by installing the Compatibility package](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Add support for AEM Forms 6.4, 6.3 and 6.2 assets in AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.5 との互換性を持たせるには、以下を実行します。

Ensure that you have [AEM Compatibility package](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) pre-installed.

1. Install the latest 6.5 [Compatibility package](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html).

   パッケージのアップロードおよびインストールについて詳しくは、「[パッケージの作業方法](/help/sites-administering/package-manager.md)」を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットに 6.5 との互換性を持たせるには、移行ユーティリティを使用します。

   For more information, see [migration utility](../../forms/using/migration-utility.md).

## 互換性パッケージをインストールすることにより AEM Forms 6.5 と互換性を持つようになったアセット {#assetsmadecompatible}

互換性パッケージをインストールすると、次のアセットとテンプレートをAEM Forms6.5と互換性のあるものにすることができます。

* AEM 6.4 以前の Correspondence Management アセット:

   * [レター](../../forms/using/create-letter.md)
   * [データディクショナリ](/help/forms/using/data-dictionary.md)
   * ドキュメントフラグメント

* アダプティブフォームの非推奨になったテンプレート：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* アダプティブフォームの非推奨になったページ

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

