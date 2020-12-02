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

対話型通信は、AEM Forms6.5で顧客とのコミュニケーションを作成するためのデフォルトで推奨されるアプローチです。AEM Forms6.5でレターを使用し続けるには、最新の[AEMFD互換パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)をインストールする必要があります。

AEMFD互換パッケージでは、AEM Forms6.5のAEM Forms6.4、6.3、6.2の次のアセットを[使用することもできます。](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨になったテンプレートおよびページ

詳しくは、[互換性パッケージ](../../forms/using/compatibility-package.md#assetsmadecompatible)をインストールして、&lt;a0/>AEM Forms6.5と互換性のあるアセットを参照してください。

## AEM Forms6.5のAEM Forms6.4、6.3、追加6.2アセットのサポート{#add-support-for-aem-forms-and-assets-in-aem-forms}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.5 との互換性を持たせるには、以下を実行します。

[AEM互換パッケージ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)がプレインストールされていることを確認します。

1. 最新の6.5 [互換性パッケージ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)をインストールします。

   パッケージのアップロードおよびインストールについて詳しくは、「[パッケージの作業方法](/help/sites-administering/package-manager.md)」を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットに 6.5 との互換性を持たせるには、移行ユーティリティを使用します。

   詳しくは、[移行ユーティリティ](../../forms/using/migration-utility.md)を参照してください。

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

