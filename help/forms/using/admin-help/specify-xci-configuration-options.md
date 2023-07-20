---
title: XCI 設定オプションの指定
description: XCI 設定オプションを指定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 7%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます。 詳しくは、 [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

デフォルトでは、Output は、次のオプションなど、XCI ファイルで指定された一部のオプションよりも優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

上記のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output ではカスタム XCI ファイルで指定された値が使用されます。

1. 管理コンソールで、 **サービス** > 出力
1. 「 Use System Default XCI Options 」チェックボックスをオンまたはオフにします。 このオプションを選択すると、Output はパケット、クリエイター、プロデューサー、compressObjectStream の設定にデフォルト値を使用します。 このオプションの選択を解除すると、Output ではカスタム XCI ファイルで指定された値が使用されます。
1. 「**保存**」をクリックします。
