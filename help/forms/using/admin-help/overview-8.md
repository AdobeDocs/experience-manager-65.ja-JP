---
title: Output サービスの概要
description: Output では、XML フォームデータを Designer で作成されたフォームデザインと結合して、様々な形式のドキュメント出力ストリームを作成できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 7%

---

# Output サービスの概要 {#overview-of-output-service}

Output では、XML フォームデータを Designer で作成されたフォームデザインと結合して、様々な形式のドキュメント出力ストリームを作成できます。 出力ストリームは、ネットワークプリンタ、ローカルプリンタ、またはディスクファイルに送信できます

管理コンソールの Output ページを使用して、Output サービスを管理できます。 設定した設定は、実行時に、対応する設定がAEM forms API で指定されていない場合に使用されます。 AEM forms SDK での設定は、管理コンソールでの設定よりも優先されます。

Output サービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_61).

管理コンソールの Output ページでは、次の複数のタスクを実行できます。

* 国際化用の文字セットを指定します。 ( 詳しくは、 [文字セットの変更](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* URL、URI、XCI、ファイルの場所の絶対パスと相対パスを指定します。 ( 詳しくは、 [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* キャッシュのサイズとポリシーを設定します。 ( 詳しくは、 [キャッシュモードの指定](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) および [キャッシュ設定の指定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* フォントをアプリケーションサーバーで使用できるようにします。 ( 詳しくは、 [フォントを使用可能にする](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* 埋め込むフォントの指定.( 詳しくは、 [埋め込むフォントの指定](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* XCI 設定オプションの指定.( 詳しくは、 [XCI 設定オプションの指定](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* セキュリティ設定の指定.( 詳しくは、 [セキュリティ設定の指定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

設定を変更した後、「保存」をクリックして、設定を「出力」に適用します。 変更を有効にするためにサーバーを再起動する必要はありませんが、キャッシュ設定を構成する際に Output サービスの再起動が必要になる場合があります。
