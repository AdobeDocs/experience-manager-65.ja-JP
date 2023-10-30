---
title: XCI 設定オプションの指定
description: XCI 設定オプションを指定する方法について説明します。 アダプティブフォームのカスタム XCI ファイル値を指定して、フォームのレンダリング中に使用することができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 64%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます。 詳しくは、 [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

デフォルトでは、Output が、以下をはじめとする XCI ファイルで指定されている一部のオプションより優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、 **サービス** > 出力
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Output では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Output では、カスタム XCI ファイルで指定された値が使用されます。
1. 「**保存**」をクリックします。
