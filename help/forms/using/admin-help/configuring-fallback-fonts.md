---
title: 代替フォントの設定
seo-title: 代替フォントの設定
description: 代替フォントの設定方法について説明します。
seo-description: 代替フォントの設定方法について説明します。
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 代替フォントの設定 {#configuring-fallback-fonts}

デフォルトのフォントがサーバーでは使用できない場合に、FontManagerResources.properties ファイルを手動で設定して、デフォルトの AEM forms のフォントを代替フォントにマップすることができます。このプロパティファイルは、adobe-fontmanager.jar ファイルにあります。

>[!NOTE]
>
>代替フォントの設定は Assembler サービスにも適用されます。

1. Navigate to the adobe-livecycle-*`[appserver]`*.ear file in the *`[aem-forms root]`*/configurationManager/export directory, make a backup copy, and unpackage the original.
1. adobe-fontmanager.jar ファイルを検索し、展開します。
1. FontManagerResources.properties ファイルを検索し、テキストエディターで開きます。
1. 必要に応じて汎用フォントと代替フォントの場所と名前を変更し、ファイルを保存します。

   The font entries in the FontManagerResources.properties file are relative to the *`[aem-forms root]`*/fonts directory. デフォルトの AEM forms フォントではないフォントを指定する場合は、このディレクトリ構造内（既存のディレクトリ内または新しく作成したディレクトリ内）にそれらのフォントをインストールする必要があります。

   >[!NOTE]
   >
   >指定したフォントまたはデフォルトのフォントに特定の Unicode 文字が含まれない場合や使用できない場合、その文字は次の優先度に従って代替フォントから取得されます。

   * ロケール固有のフォント
   * ロケールが設定されていない場合は ROOT フォント
   * 代替テーブルで設定された順序で検索される汎用フォント

1. adobe-fontmanager.jar ファイルを再パッケージ化します。
1. Repackage the adobe-livecycle-*`[appserver]`*.ear file and then redeploy it either manually or by running Configuration Manager.

>[!NOTE]
>
>Do not use Configuration Manager to repackage the adobe-livecycle-`[appserver]`.ear file because it will overwrite your modifications with the AEM forms default values.

