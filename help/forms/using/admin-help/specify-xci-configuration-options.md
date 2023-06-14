---
title: XCI 設定オプションの指定
description: XCI 設定オプションを指定する方法について説明します。
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 12%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます。 ( [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) デフォルトでは、Output は、次のオプションなど、XCI ファイルで指定された一部のオプションよりも優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

上記のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output ではカスタム XCI ファイルで指定された値が使用されます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「 Use System Default XCI Options 」チェックボックスをオンまたはオフにします。 このオプションを選択すると、Output はパケット、クリエイター、プロデューサー、compressObjectStream の設定にデフォルト値を使用します。 このオプションの選択を解除すると、Output ではカスタム XCI ファイルで指定された値が使用されます。
1. 「保存」をクリックしてください。
