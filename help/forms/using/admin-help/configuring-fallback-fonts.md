---
title: 代替フォントの設定
description: AEM Forms 用に代替フォントを設定する方法について説明します。FontManagerResources.properties ファイルを使用して、デフォルトのフォントを代替フォントに手動でマップすることができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---

# 代替フォントの設定 {#configuring-fallback-fonts}

デフォルトのフォントがサーバーでは使用できない場合に、FontManagerResources.properties ファイルを手動で設定して、デフォルトの AEM Forms のフォントを代替フォントにマップすることができます。このプロパティファイルは、adobe-fontmanager.jar ファイルにあります。

>[!NOTE]
>
>代替フォントの設定は Assembler サービスにも適用されます。

1. *`[aem-forms root]`*/configurationManager/export ディレクトリにある adobe-livecycle-*`[appserver]`*.ear ファイルに移動し、バックアップコピーを作成して元のファイルを展開します。
1. adobe-fontmanager.jar ファイルを検索し、展開します。
1. FontManagerResources.properties ファイルを検索し、テキストエディターで開きます。
1. 必要に応じて汎用フォントと代替フォントの場所と名前を変更し、ファイルを保存します。

   FontManagerResources.properties ファイルのフォントエントリは、*`[aem-forms root]`*/fonts ディレクトリからの相対パスで指定されます。デフォルトの AEM Forms フォントではないフォントを指定する場合は、このディレクトリ構造内（既存のディレクトリ内または新しく作成したディレクトリ内）にそれらのフォントをインストールする必要があります。

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
