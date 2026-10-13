---
title: 互換性パッケージ
description: AEM Forms 6.5 に互換性パッケージをインストールすると、AEM Forms 6.4 以前のバージョンの Correspondence Management アセットと、非推奨のアダプティブフォームテンプレートおよびページが使用できるようになります
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 91%
---
# 互換性パッケージ{#compatibility-package}

## 概要 {#overview}

インタラクティブ通信は、AEM Forms 6.5でお客様とのコミュニケーションを作成する際にデフォルトで推奨される方法です。 AEM Forms 6.5で引き続き文字を使用するには、最新の[AEMFD互換性パッケージ &#x200B;](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)をインストールする必要があります。

AEMFD 互換性パッケージを使用すると、[AEM Forms 6.5 で、AEM Forms 6.4、6.3、6.2 の次のアセットも使用できます。](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨（廃止予定）になったテンプレートおよびページ

詳細については、[互換性パッケージをインストールすることにより AEM Forms 6.5 と互換性を持つようになったアセット](../../forms/using/compatibility-package.md#assetsmadecompatible)を参照してください。

## AEM Forms 6.5 で AEM Forms 6.4、6.3 および 6.2 のアセットのサポートを追加 {#add-support-for-aem-forms-and-assets-in-aem-forms}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.5 との互換性を持たせるには、以下を実行します。

[AEM 互換性パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)が事前にインストールされていることを確認します。

1. 最新の 6.5 [互換性パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)をインストールします。

   パッケージのアップロードおよびインストールについて詳しくは、[パッケージの操作方法](/help/sites-administering/package-manager.md)を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットに 6.5 との互換性を持たせるには、移行ユーティリティを使用します。

   >[!NOTE]
   >
   > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

   詳しくは、[移行ユーティリティ](../../forms/using/migration-utility.md)を参照してください。

## 互換性パッケージをインストールすることにより AEM Forms 6.5 と互換性を持つようになったアセット {#assetsmadecompatible}

互換性パッケージをインストールすると、以下のアセットとテンプレートに AEM Forms 6.5 との互換性を保持できます。

* AEM 6.4 以前の Correspondence Management アセット:

  * [レター](../../forms/using/create-letter.md)
  * [データディクショナリ](/help/forms/using/data-dictionary.md)
  * ドキュメントフラグメント

* アダプティブフォームの非推奨になったテンプレート:

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
