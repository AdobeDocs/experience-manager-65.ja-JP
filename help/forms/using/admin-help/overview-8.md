---
title: Output サービスの概要
description: Output では、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 100%

---

# Output サービスの概要 {#overview-of-output-service}

Output では、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成できます。出力ストリームは、ネットワークプリンター、ローカルプリンターまたはディスクファイルに送信できます。

管理コンソールの Output ページを使用して、Output サービスを管理できます。ここで指定した設定は、AEM Forms API で同等の設定が指定されていない場合に、実行時に使用されます。AEM Forms SDK による設定は、管理コンソールを使用して指定した設定よりも優先されます。

Output サービスについて詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_61)を参照してください。

管理コンソールの Output ページでは、次の複数のタスクを実行できます。

* 国際化対応文字セットの指定（[文字セットの変更](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)を参照）。
* URL、URI、XCI およびファイルの場所の絶対パスと相対パスの指定（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。
* キャッシュサイズおよびポリシーの設定（[キャッシュモードの指定](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)および[キャッシュ設定の指定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)を参照）。
* アプリケーションサーバーでフォントを使用可能にする（[フォントを使用可能にする](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)を参照）。
* 埋め込むフォントの指定.（[埋め込むフォントの指定](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)を参照）。
* XCI 設定オプションの指定.（[XCI 設定オプションの指定](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)を参照）。
* セキュリティ設定の指定.（[セキュリティ設定の指定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)を参照）。

設定を変更した後、「保存」をクリックして Output に変更を適用します。変更内容はサーバーを再起動しなくても有効になります。ただし、キャッシュ設定を指定した場合は、Output サービスの再起動が必要になる場合があります。
