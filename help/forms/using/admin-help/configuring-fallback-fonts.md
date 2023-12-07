---
title: 代替フォントの設定
description: AEM Formsのフォールバックフォントを設定する方法を説明します。 FontManagerResources.properties ファイルを使用すると、デフォルトのフォントをフォールバックフォントに手動でマッピングできます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 29%

---

# 代替フォントの設定 {#configuring-fallback-fonts}

デフォルトのフォントがサーバー上で使用できない場合に、デフォルトのAEM forms フォントをフォールバック（または代替）にマップするように、FontManagerResources.properties ファイルを手動で設定できます。 このプロパティファイルは、 adobe-fontmanager.jar ファイルにあります。

>[!NOTE]
>
>フォールバックフォントの設定は、Assembler サービスにも適用されます。

1. *`[aem-forms root]`*/configurationManager/export ディレクトリにある adobe-livecycle-*`[appserver]`*.ear ファイルに移動し、バックアップコピーを作成して元のファイルを展開します。
1. adobe-fontmanager.jar ファイルを探し、パッケージ化を解除します。
1. FontManagerResources.properties ファイルを見つけ、テキストエディターで開きます。
1. 汎用フォントとフォールバックフォントの場所と名前を必要に応じて変更し、ファイルを保存します。

   FontManagerResources.properties ファイルのフォントエントリは、*`[aem-forms root]`*/fonts ディレクトリからの相対パスで指定されます。デフォルトのAEM forms フォント以外のフォントを指定する場合は、このディレクトリ構造内（既存のディレクトリ内または新しく作成されたディレクトリ内）に、これらのフォントをインストールする必要があります。

   >[!NOTE]
   >
   >指定したフォントまたはデフォルトのフォントに特定の Unicode 文字が含まれていない場合、または使用できない場合、その文字は次の優先順位に従ってフォールバックフォントから取得されます。

   * ロケール固有のフォント
   * ロケールが設定されていない場合は ROOT フォント
   * フォールバックテーブルで設定された順序で検索される汎用フォント

1. adobe-fontmanager.jar ファイルを再パッケージ化します。
1. adobe-livecycle-*`[appserver]`*.ear ファイルを再パッケージ化し、手動で実行するか、または Configuration Manager を実行して、再デプロイします。

>[!NOTE]
>
>AEM Forms のデフォルト値を使用して変更内容が上書きされるので、Configuration Manager を使用して adobe-livecycle-`[appserver]`.ear ファイルを再パッケージ化しないでください。
