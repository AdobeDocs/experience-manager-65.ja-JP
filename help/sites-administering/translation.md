---
title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツを翻訳する方法を説明します。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
source-git-commit: 3f5173c0c2b17e8cf560753088451f78c6529f5c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 83%

---

# 多言語サイトのコンテンツの翻訳 {#translating-content-for-multilingual-sites}

ページコンテンツ、アセット、ユーザー生成コンテンツの翻訳を自動化して、多言語の Web サイトを作成および管理します。 翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* 人間による翻訳：コンテンツが翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。翻訳が完了すると、翻訳済みコンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM に統合されると、コンテンツは AEM と翻訳プロバイダーの間で自動的に送信されます。
* 機械翻訳：機械翻訳サービスでは、コンテンツがすぐに翻訳されます。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。
1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md#configuring-pages-for-translation)ます。
1. 翻訳する[コンテンツのタイプを特定](/help/sites-administering/tc-rules.md)します。
1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳プロジェクトを作成](/help/sites-administering/tc-manage.md)して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

AEM との統合のためのコネクタが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーが projects-administrators グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)には、実装に関する重要な情報が記載されています。
