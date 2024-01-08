---
title: Forms 設定の基本事項
description: インタラクティブなデータキャプチャアプリケーションを作成するのに役立つ様々なフォームサービスについて説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# Forms 設定の基本事項 {#basics-of-configuring-forms}

Formsサービスを使用すると、通常 Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々な形式でレンダリングする、単一のフォームデザインを作成します。

* Adobe ReaderまたはブラウザーでのPDFとして
* XHTML 1.0 に準拠したレンダリングを含む、様々なブラウザー環境でのHTMLとして
* をフォームガイドとして使用します。これは、AdobeFlash Playerをサポートする様々なブラウザ環境で使用されます。

Formsサービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

管理コンソールのFormsページを使用して、Formsサービスの動作を設定できます。 これらの設定は、サービスのすべての呼び出しに適用されます。 AEM forms SDK を通じて送信されるパラメーターは、管理コンソールで設定された設定より優先されますが、影響を受けるのは特定の呼び出しのみです。

管理コンソールでForms設定を変更したら、「保存」をクリックします。 変更を有効にするために、サーバーを再起動する必要はありません。 ただし、キャッシュモードの設定を行う場合は、Formsサービスの停止と再起動が必要になる場合があります。 （[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください。）
