---
title: Output サービスの概要
description: Output では、XML フォームデータを、Designer で作成されたフォームデザインに結合して、様々な形式でドキュメント出力ストリームを作成できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 100%
---
# Output サービスの概要 {#overview-of-output-service}

Output では、XML フォームデータを、Designer で作成されたフォームデザインに結合して、様々な形式でドキュメント出力ストリームを作成できます。 出力ストリームは、ネットワークプリンター、ローカルプリンターまたはディスクファイルに送信できます。

管理コンソールの Output ページを使用して、Output サービスを管理できます。 ここで指定した設定は、AEM Forms API で同等の設定が指定されていない場合に、実行時に使用されます。 AEM Forms SDK による設定は、管理コンソールを使用して指定した設定よりも優先されます。

Output サービスについて詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_61)を参照してください。

管理コンソールの Output ページでは、次の複数のタスクを実行できます。

* 国際化のための文字セットを指定します。 （[文字セットの変更](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)を参照）。
* URL、URI、XCI およびファイルの場所の絶対パスと相対パスの指定 （[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。
* キャッシュサイズおよびポリシーの設定 （[キャッシュモードの指定](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)および[キャッシュ設定の指定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)を参照）。
* アプリケーションサーバーでフォントを使用可能にする （[フォントを使用可能にする](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)を参照）。
* 埋め込むフォントの指定 （[埋め込むフォントの指定](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)を参照）。
* XCI 設定オプションの指定. （[XCI 設定オプションの指定](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)を参照）。
* セキュリティ設定の指定. （[セキュリティ設定の指定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)を参照）。

設定を変更した後、「保存」をクリックして Output に変更を適用します。 変更内容はサーバーを再起動しなくても有効になります。ただし、キャッシュ設定を指定した場合は、Output サービスの再起動が必要になる場合があります。
