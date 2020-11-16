---
title: XCI 設定オプションの指定
seo-title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。
seo-description: XCI 設定オプションの指定方法について説明します。
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 100%

---


# XCI 設定オプションの指定 {#specifying-xci-configuration-options}

Forms では、レンダリングに使用するカスタム XCI ファイルを指定できます（[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。デフォルトでは、以下をはじめとする XCI ファイルで指定されている一部のオプションは Forms によって上書きされます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Forms では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Forms では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Forms では、カスタム XCI ファイルで指定された値が使用されます。
1. 「保存」をクリックします。

