---
title: 繰り返し可能なセクションを使用したフォームの作成
seo-title: 繰り返し可能なセクションを使用したフォームの作成
description: 繰り返し可能なセクションとは、フォームに動的に追加またはフォームから動的に削除できるパネルのことです。
seo-description: 繰り返し可能なセクションとは、フォームに動的に追加またはフォームから動的に削除できるパネルのことです。
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 77%

---


# 繰り返し可能なセクションを使用したフォームの作成  {#creating-forms-with-repeatable-sections}

繰り返し可能なセクションとは、フォームに動的に追加またはフォームから動的に削除できるパネルのことです。

例えば、就職活動の場合、求職者は前職の詳細を提供するにあたり、会社名、役職、担当していたプロジェクト、その他備考などに情報を区分けします。すべての雇用者の情報は当然異なっていますが、セクションの構成は似通っています。そのような場合には、求人応募フォームに雇用者セクションを 1 つ設けておいて、さらに必要に応じてそのようなセクションを動的に追加できるようにしておきます。動的に追加できるこれらのセクションを、繰り返し可能なセクションといいます。

以下に挙げる方法のうちいずれかによって、繰り返し可能なパネルを作成できます。

## スクリプトを通じたインスタンスマネージャーの使用  {#using-instance-manager-via-scripts-nbsp}

1. 編集モードで、パネルを選択し、![cmpr](assets/cmppr.png)をタップします。 サイドバーのプロパティで「**パネルを繰り返し可能にする**」を有効にします。「**[!UICONTROL 最大]**」フィールドと「**[!UICONTROL 最小]**」フィールドに値を指定します。

   最大数フィールドでは、パネルがそのページ上に登場してよい最大の回数を指定します。パネルの登場回数を制限しないように設定するには、最大数フイールドに「-1」を入力します。

   最小数フィールドでは、パネルがそのフォーム上に登場してよい最小の回数を指定します。後で最小数フィールドの値に「0」を指定した場合は、レンダリング完了後にスクリプトを介してすべてのインスタンスを削除することができます。

   >[!NOTE]
   >
   >繰り返しを許可しないパネルを作成するには、最大数フィールドと最小数フィールドに 1 を入力します。アコーディオンレイアウトの場合は、最大数フィールドに「-1」を指定することはできません。この場合は任意の高い数値を入力することにより、最大数を制限しない設定と同様の動作を実現します。

1. パネルの親要素に繰り返しを許可する場合は、繰り返し可能なパネルのインスタンスを管理するために追加ボタンおよび削除ボタンが親要素に含まれている必要があります。次の手順を実行して、親にボタンを挿入し、ボタンのスクリプトを有効にします。

   1. サイドバーから、ボタンコンポーネントをパネルの親要素にドラッグ＆ドロップします。コンポーネントを選択し、![edit-rules](assets/edit-rules.png)をタップします。 ルールエディターでボタンのルールが開きます。
   1. ルールエディターウィンドウで、「**作成**」をクリックします。

      「フォームオブジェクトと関数」の行で、「**ビジュアルエディター**」を選択します。

      1. ルール領域のWHENで、**がクリックされた状態を選択します。**
      1. THENで、次の操作を行います。

         * パネルを追加ボタンを作成するには、「**インスタンス追加**」を選択し、![トグルサイドパネル](assets/toggle-side-panel.png)を使用してパネルをドラッグ&amp;ドロップするか、**オブジェクトをドロップまたは次から選択します。**
         * パネルを削除ボタンを作成するには、「**インスタンスを削除**」を選択し、![トグルサイドパネル](assets/toggle-side-panel.png)を使用してパネルをドラッグ&amp;ドロップするか、**オブジェクトをドロップまたは次から選択します。**

      フォームオブジェクトと関数の行で、「**コードエディター**」を選択します。「**ルールを編集**」をクリックし、コード領域で次の操作を行います。

      * パネルを追加ボタンを作成するには、`this.panel.instanceManager.addInstance()`()を指定します。
      * パネルを削除ボタンを作成するには、`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`を指定します

      「**完了**」をクリックします。

      >[!NOTE]
      >
      >フィールドが繰り返し可能パネルに属する場合、スクリプトで名前を指定して直接アクセスすることはできません。フィールドにアクセスするには、`InstanceManager`の`instances` APIを使用して、フィールドが属する繰り返し可能なインスタンスを指定します。 `InstanceManager`で`instances` APIを使用する構文は次のとおりです。
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例えば、テキストボックス付きの繰り返し可能パネルを持つアダプティブフォームを作成するとします。このフォームに 3 つの繰り返し可能テキストボックスを事前入力するには、以下の xml が必要です。
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >AA1 データを読み込むには次のように指定します。
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >AA2 データを読み込むには次のように指定します。
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >詳しくは、[AEM Forms Java API リファレンス](https://adobe.com/go/learn_aemforms_documentation_63)の「Class: InstanceManager#instances」を参照してください。

      >[!NOTE]
      >
      >パネルのすべてのインスタンスがアダプティブフォームから削除された場合、削除されたパネルのインスタンスを追加するには、_panelName構文を使用してパネルのインスタンスマネージャーを取り込み、インスタンスマネージャーのaddInstance APIを使用して削除されたインスタンスを追加します。 例えば、_panelName.addInstance() は削除されたパネルのインスタンスを 1 つ追加します。















## 親パネルに対するアコーディオンレイアウトの使用{#using-the-accordion-layout-for-the-parent-panel-nbsp}

1 つのパネルにはさまざまなレイアウトを選択することができます。アコーディオンデザインのレイアウトでは、繰り返し可能パネルをただちに使用することができます。アコーディオンデザインのレイアウトで繰り返し可能パネルを使用するには、以下の手順を実行します。

1. 繰り返しを許可するパネルの親要素上で、![cmppr](assets/cmppr.png)をタップします。 サイドバーにプロパティが表示されます。**レイアウト**&#x200B;ドロップダウンで、「**アコーディオン**」を選択します。
1. 繰り返しを許可するパネルで、![cmpr](assets/cmppr.png)をタップします。 サイドバーにパネルのプロパティが表示されます。「**パネルを繰り返し可能にする**」タブを有効にし、**最大数**&#x200B;および&#x200B;**最小数**&#x200B;フィールドの値を指定します。

   これで、プラス(+)ボタンと削除（![削除 — パネル](assets/delete-panel.png)）ボタンを使用して、パネルの追加と削除を行うことができます。

## フォームテンプレート（XDP/XSD）からのサブフォームの繰り返しの使用{#using-repeating-subforms-from-form-template-xdp-xsd}

繰り返し可能なサブフォームは、アダプティブフォームにおける繰り返し可能なパネルに似ています。AEM Formsデザイナーで、次の手順を実行して繰り返しサブフォームを作成します。

1. 階層パレットで、繰り返しを許可するサブフオームの親サブフォームを選択します。
1. オブジェクトパレットの「サブフォーム」タブをクリックし、コンテンツリストで「フローレイアウト」を選択します。
1. 繰り返すサブフォームを選択します。
1. オブジェクトパレットで「サブフォーム」タブをクリックし、コンテンツリストで「配置済み」または「フローレイアウト」を選択します。
1. 「連結」タブをクリックし、「各データアイテムについて行を繰り返す」を選択します。
1. 繰り返し回数の最小値を指定する場合は、「最小値」を選択して関連するボックスに数値を入力します。このオプションを 0 に設定した場合は、データマージ時にサブフォーム内のオブジェクトにデータが提供されないと、フォームのレンダリング時にサブフォームが配置されません。
1. サブフォームの繰り返し回数の最大値を指定する場合は、「最大値」を選択して関連するボックスに数値を入力します。「最大値」に値を入力しなければ、サブフォームの繰り返し回数は無制限になります。
1. サブフォームの繰り返し回数をデータ量に関係なく指定する場合は、「初期値」オプションを選択して、関連するボックスに数値を入力します。このオプションを選択した場合は、データが使用できないときやデータ項目が指定された「初期値」の値より少ないときにも、フォーム上に空のサブフォームインスタンスが配置されます。
1. 親サブフオームにボタンを 2 つ追加します。ひとつはインスタンスの追加に、もうひとつは繰り返し可能なサブフォームのインスタンスの削除に使用します。詳しい手順については、「[アクションの作成](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)」を参照してください。
1. ここで、アダプティブフォームにフォームテンプレートをリンクします。詳しい手順については、「[テンプレートに基づくアダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template)」を参照してください。
1. 手順 9 で作成したボタンを使用して、サブフォームを追加および削除します。

添付の .zip ファイルには、繰り返し可能なサブフォーラムのサンプルが含まれています。

[ファイルを入手](assets/samplerepeatablesubform.zip)

## XML Schema（XSD）の繰り返し設定の使用{#using-repeat-settings-of-an-xml-schema-xsd-br}

XML Schema、または任意の複合タイプエレメントの minOccours および maxOccurs プロパティから繰り返し可能なパネルを作成できます。「[XML Schema をフォームモデルとして使用する場合のアダプティブフォームの作成](/help/forms/using/adaptive-form-xml-schema-form-model.md)」を参照してください。

以下のコードでは、`SampleType` パネルで minOccours および maxOccurs プロパティが使用されています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>アコーディオンデザインではないレイアウトの場合は、インスタンスの追加と削除を行うには、アダプティブフォームのボタンコンポーネントを使用します。
