---
title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 21%

---

# XCI 設定オプションの指定 {#specifying-xci-configuration-options}

Formsでは、レンダリングに使用できるカスタム XCI ファイルを指定できます。 ( 詳しくは、 [Formsの場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) デフォルトでは、Formsは、次のオプションを含む XCI ファイルで指定された一部のオプションを上書きします。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

上記のオプションの上書きをキャンセルするオプションを選択できます。この場合、Formsはカスタム XCI ファイルで指定された値を使用します。

1. 管理コンソールで、 **サービス** > **Forms**.
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Formsはパケット、作成者、プロデューサー、compressObjectStream の設定にデフォルト値を使用します。 このオプションの選択を解除すると、Formsはカスタム XCI ファイルで指定された値を使用します。
1. 「**保存**」をクリックします。
