---
title: XCI 設定オプションの指定
seo-title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。
seo-description: XCI 設定オプションの指定方法について説明します。
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 100%

---


# XCI 設定オプションの指定 {#specify-xci-configuration-options}

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。デフォルトでは、Output が、以下をはじめとする XCI ファイルで指定されている一部のオプションより優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Output では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Output では、カスタム XCI ファイルで指定された値が使用されます。
1. 「保存」をクリックします。

