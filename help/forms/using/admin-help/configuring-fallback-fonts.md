---
title: 代替フォントの設定
description: AEM Forms 用に代替フォントを設定する方法について説明します。 FontManagerResources.properties ファイルを使用して、デフォルトのフォントを代替フォントに手動でマップすることができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 100%
---
# 代替フォントの設定 {#configuring-fallback-fonts}

デフォルトのフォントがサーバーでは使用できない場合に、FontManagerResources.properties ファイルを手動で設定して、デフォルトの AEM Forms のフォントを代替フォントにマップすることができます。 このプロパティファイルは、adobe-fontmanager.jar ファイルにあります。

>[!NOTE]
>
>代替フォントの設定はアセンブラーサービスにも適用されます。

1. *`[aem-forms root]`*/configurationManager/export ディレクトリにある adobe-livecycle-*`[appserver]`*.ear ファイルに移動し、バックアップコピーを作成して元のファイルを展開します。
1. adobe-fontmanager.jar ファイルを検索し、展開します。
1. FontManagerResources.properties ファイルを検索し、テキストエディターで開きます。
1. 必要に応じて汎用フォントと代替フォントの場所と名前を変更し、ファイルを保存します。

   FontManagerResources.properties ファイルのフォントエントリは、*`[aem-forms root]`*/fonts ディレクトリからの相対パスで指定されます。 デフォルトの AEM Forms フォントではないフォントを指定する場合は、このディレクトリ構造内（既存のディレクトリ内または新しく作成したディレクトリ内）にそれらのフォントをインストールする必要があります。

   >[!NOTE]
   >
   >指定したフォントまたはデフォルトのフォントに特定の Unicode 文字が含まれない場合や使用できない場合、その文字は次の優先度に従って代替フォントから取得されます。

   * ロケール固有のフォント
   * ロケールが設定されていない場合は ROOT フォント
   * 代替テーブルで設定された順序で検索される汎用フォント

1. adobe-fontmanager.jar ファイルを再パッケージ化します。
1. adobe-livecycle-*`[appserver]`*.ear ファイルを再パッケージ化し、手動で実行するか、または Configuration Manager を実行して、再デプロイします。

>[!NOTE]
>
>AEM Forms のデフォルト値を使用して変更内容が上書きされるので、Configuration Manager を使用して adobe-livecycle-`[appserver]`.ear ファイルを再パッケージ化しないでください。
