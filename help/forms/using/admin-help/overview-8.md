---
title: Output サービスの概要
seo-title: Output サービスの概要
description: Output では、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成できます。
seo-description: Output では、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成できます。
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 97%

---


# Output サービスの概要 {#overview-of-output-service}

Output では、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成できます。出力ストリームは、ネットワークプリンター、ローカルプリンターまたはディスクファイルに送信できます。

管理コンソールの Output ページを使用して、Output サービスを管理できます。ここで設定した値は、対応する値が AEM Forms API から設定されていない場合にのみ、実行時に使用されます。AEM Forms SDK による設定は、管理コンソールでの設定よりも優先されます。

Output サービスについて詳しくは、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_61)」を参照してください。

管理コンソールの Output ページでは、以下の複数のタスクを実行できます。

* 国際化対応文字セットの指定（[文字セットの変更](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)を参照）。
* URL、URI、XCI およびファイルの場所の絶対パスと相対パスの指定（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。
* キャッシュサイズおよびポリシーの設定（[キャッシュモードの指定](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)および[キャッシュ設定の指定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)を参照）。
* アプリケーションサーバーでフォントを使用できるようにします（[フォントを使用可能にする](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)を参照）。
* 埋め込むフォントの指定（[埋め込むフォントの指定](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)を参照）。
* XCI 設定オプションの指定（[XCI 設定オプションの指定](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)を参照）。
* セキュリティ設定の指定（[セキュリティ設定の指定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)を参照）。

設定を変更した後、「保存」をクリックして Output に変更を適用します。変更内容はサーバーを再起動しなくても有効になります。ただし、キャッシュ設定を指定した場合は、Output サービスの再起動が必要になる場合があります。
