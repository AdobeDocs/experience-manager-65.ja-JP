---
title: カスタムフォームマッピングの作成
description: Adobe Campaignでカスタムテーブルを作成する場合、AEMでそのカスタムテーブルにマッピングするフォームを作成する必要が生じる場合があります
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 19%

---

# カスタムフォームマッピングの作成{#creating-custom-form-mappings}

Adobe Campaignでカスタムテーブルを作成する場合、AEMでそのカスタムテーブルにマッピングするフォームを作成する必要が生じる場合があります。

このドキュメントでは、カスタムフォームマッピングを作成する方法について説明します。 このドキュメントの手順を完了すると、ユーザーが今後のイベントに新規登録できるイベントページが表示されます。 その後、Adobe Campaignを通じて、これらのユーザーをフォローアップします。

## 前提条件 {#prerequisites}

以下をインストールする必要があります。

* Adobe Experience Manager
* Adobe Campaign Classic

詳しくは、[AEM と Adobe Campaign Classic の統合](/help/sites-administering/campaignonpremise.md)を参照してください。

## カスタムフォームマッピングの作成 {#creating-custom-form-mappings-2}

カスタムフォームマッピングを作成するには、次の大まかな手順に従う必要があります。手順については、以下の節で詳しく説明します。

1. カスタムテーブルを作成します。
1. の拡張 **シード** 表。
1. カスタムマッピングを作成します。
1. カスタムマッピングに基づいて配信を作成します。
1. 作成した配信を使用するAEMでフォームを作成します。
1. フォームを送信してテストします。

### Adobe Campaignでのカスタムテーブルの作成 {#creating-the-custom-table-in-adobe-campaign}

まず、Adobe Campaignでカスタムテーブルを作成します。 この例では、以下の定義を使用して、イベントテーブルを作成します。

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

イベントテーブルを作成したら、 **データベース構造の更新ウィザード** をクリックして、テーブルを作成します。

### シードテーブルの拡張 {#extending-the-seed-table}

Adobe Campaignで、 **追加** の拡張を作成するには、以下を実行します。 **シードアドレス (nms)** 表。

![chlimage_1-194](assets/chlimage_1-194.png)

今度は&#x200B;**イベント**&#x200B;テーブルのフィールドを使用して、**シード**&#x200B;テーブルを拡張します。

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

この後、を実行します。 **データベース更新ウィザード** 変更を適用します。

### カスタムターゲットマッピングの作成 {#creating-custom-target-mapping}

In **管理/キャンペーン管理** t、に移動します。 **ターゲットマッピング** 新しい T を追加します。**ターゲットマッピング。**

>[!NOTE]
>
>次に対して意味のある名前を使用してください。 **内部名**.

![chlimage_1-195](assets/chlimage_1-195.png)

### カスタム配信テンプレートの作成 {#creating-a-custom-delivery-template}

この手順では、作成した **ターゲットマッピング**.

In **リソース/テンプレート**「配信テンプレート」に移動し、既存のAEM配信を複製します。 クリック時 **宛先**、「イベントを作成」を選択します。 **ターゲットマッピング**.

![chlimage_1-196](assets/chlimage_1-196.png)

### AEMでのフォームの構築 {#building-the-form-in-aem}

AEMで、でCloud Serviceを設定していることを確認します。 **ページのプロパティ**.

その後、「**Adobe Campaign**」タブで、「[カスタム配信テンプレートの作成](#creating-a-custom-delivery-template)」で作成した配信を選択します。

![chlimage_1-197](assets/chlimage_1-197.png)

フィールドを設定する際は、フォームフィールドに一意の要素名を必ず指定してください。

フィールドを設定した後、マッピングを手動で変更する必要があります。

CRXDE Lite で、 **jcr:content** （ページの）ノードに追加し、 **acMapping** の値を **ターゲットマッピング**.

![chlimage_1-198](assets/chlimage_1-198.png)

フォームの設定で、「存在しない場合は作成」チェックボックスをオンにします。

![chlimage_1-199](assets/chlimage_1-199.png)

### フォームの送信 {#submitting-the-form}

これで、フォームを送信し、値が保存されているかどうかをAdobe Campaign側で検証できます。

![chlimage_1-200](assets/chlimage_1-200.png)

## トラブルシューティング {#troubleshooting}

**&quot;要素「@eventdate」の値「02/02/2015」のタイプが無効です ( タイプ「Event」のドキュメント ([adb:event])&#39;)&quot;**

フォームを送信する際に、このエラーは **error.log** AEMの

これは、日付フィールドの形式が無効なためです。 回避策は、 **yyyy-mm-dd** を値として使用します。
