---
title: AEM 6.5 Forms へのアップグレード
seo-title: AEM 6.5 Forms へのアップグレード
description: AEM 6.3 Forms および AEM 6.4 Forms から AEM 6.5 Forms に直接アップグレードすることができます。
seo-description: AEM 6.3 Forms および AEM 6.4 Forms から AEM 6.5 Forms に直接アップグレードすることができます。
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 100%

---


# AEM 6.5 Forms へのアップグレード{#upgrade-to-aem-forms}

AEM 6.5 Forms には、いくつかの新機能と機能強化が導入されています。これにより、フォームと通信の作成、管理、ユーザーエクスペリエンスが簡素化されます。AEM 6.5 Forms のすべての新機能と機能強化については、[新機能の概要についてのドキュメント](../../forms/using/whats-new.md)を参照してください。

既存の LiveCycle または AEM Forms のインストール環境をアップグレードすると、AEM 6.5 Forms に導入された新機能と機能強化を使用できるようになります。既存のデータ、プロセス、アセットはそのまま保存されます。また、プロセスのメタデータと状態についても、そのまま保存されます。アップグレードを行うためのアップグレードパスは、選択することができます。

以下の図は、OSGi 上の AEM Forms の有効なアップグレードパスを示しています。

![](do-not-localize/osgi-upgrade-path.png)

以下の場合は、直接アップグレードすることができます。

* OSGi 上の AEM 6.3 Forms
* OSGi 上の AEM 6.4 Forms

以下の場合は、マルチホップアップグレードを実行することができます。

* OSGi 上の AEM 6.0 Forms
* OSGi 上の AEM 6.1 Forms
* OSGi 上の AEM 6.2 Forms

以下の図は、JEE 上の AEM Forms の有効なアップグレードパスを示しています。

![](do-not-localize/jee-upgrade-6-5.png)

以下の場合は、直接アップグレードすることができます。

* JEE 上の AEM 6.3 Forms
* JEE 上の AEM 6.4 Forms

以下の場合は、マルチホップアップグレードを実行することができます。

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* JEE 上の AEM 6.0 Forms
* JEE 上の AEM 6.1 Forms
* JEE 上の AEM 6.2 Forms

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
