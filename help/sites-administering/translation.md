---
title: 多言語サイトのコンテンツの翻訳
seo-title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツの翻訳方法について説明します。
seo-description: 多言語サイトのコンテンツの翻訳方法について説明します。
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 87%

---


# 多言語サイトのコンテンツの翻訳 {#translating-content-for-multilingual-sites}

ページコンテンツ、アセットおよびユーザー生成コンテンツの翻訳を自動化して、多言語の Web サイトを作成および管理します。翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* 人間による翻訳：コンテンツが翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。完了すると、翻訳コンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。
* 機械翻訳：機械翻訳サービスでは、コンテンツがすぐに翻訳されます。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。
1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md#configuring-pages-for-translation)ます。
1. [翻訳するコンテンツのタイプを特定します](/help/sites-administering/tc-rules.md) 。
1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳プロジェクトを作成し](/help/sites-administering/tc-manage.md) 、翻訳対象のコンテンツを収集して翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

AEM との統合のためのコネクターが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーはプロジェクト管理者グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

The [Translation Best Practices](/help/sites-administering/tc-bp.md) page contains important information regarding your implementation.
