---
title: 文字セットの変更
description: 出力ストリームのエンコードに使用する文字セットを指定できます。 文字セットを変更する方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 63%

---

# 文字セットの変更 {#change-the-character-set}

出力ストリームのエンコードに使用する文字セットを指定できます。

1. 管理コンソールで、**[!UICONTROL サービス／Output]** をクリックします。
1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、API 経由で指定する `TransformationFormat` と `PrintFormat` の値によって異なります。リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   `TransformationFormat` が PDF か PDF/A である場合、または `PrintFormat` が PCL、PostScript、Zebra Label、IPL、DPL、TPCL、GenericColorPCL または GenericPSLevel3 である場合、特定の文字セットのみがサポートされます。

   文字セットは、有効な正規名である必要があります。 デフォルト値は ISO-8859-1 です。

1. 「**[!UICONTROL 保存]**」をクリックします。
