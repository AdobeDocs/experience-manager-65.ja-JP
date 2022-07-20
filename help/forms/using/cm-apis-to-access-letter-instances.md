---
title: レターインスタンスにアクセスするための API
seo-title: APIs to access letter instances
description: レターインスタンスにアクセスするための API を使用する方法について説明します。
seo-description: Learn how to use APIs to access letter instances.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 100%

---

# レターインスタンスにアクセスするための API {#apis-to-access-letter-instances}

## 概要 {#overview}

Correspondence Management の「通信を作成」UI を使用して、作成中のレターインスタンスのドラフトを保存することができます。また、この UI には送信済みのレターインスタンスが存在します。

Correspondence Management には、送信済みまたはドラフトのレターインスタンスを取り扱うための一覧表示インターフェイスを構築できる API が用意されています。この API は、エージェントの送信済みとドラフトのレターインスタンスを一覧表示して開きます。これにより、エージェントはドラフトまたは送信済みのレターインスタンスで作業を続行することができます。

## レターインスタンスの取得 {#fetching-letter-instances}

Correspondence Management は API を使用して、LetterInstanceService サービスからレターインスタンスを取得します。

| メソッド | 説明 |
|--- |--- |
| getAllLetterInstances | 入力クエリパラメーターに基づいてレターインスタンスを取得します。すべてのレターインスタンスを取得するには、クエリパラメーターをヌルとして渡します。 |
| getLetterInstance | レターインスタンス ID に基づいて指定したレターインスタンスを取得します。 |
| letterInstanceExists | LetterInstance が指定した名前で存在するかどうかをチェックします。 |

>[!NOTE]
>
>LetterInstanceService は OSGI サービスであり、そのインスタンスは Java クラスの @Reference を使用して、
>または JSP の sling.getService(LetterInstanceService.クラス）を使用して取得できます。

### getAllLetterInstances の使用 {#using-nbsp-getallletterinstances}

下記の API は、クエリオブジェクトに基づいてレターインスタンスを検索します（送信済みとドラフトの両方）。クエリオブジェクトが null の場合、すべてのレターインスタンスを返します。この API は [LetterInstanceVO](https://helpx.adobe.com/jp/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) オブジェクトの一覧を返します。この一覧は、レターインスタンスの追加情報の抽出に使用することができます。

**構文**： `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>query パラメーターは、レターインスタンスの検索またはフィルタリングに使用されます。ここで、クエリはオブジェクトの最上位の属性またはプロパティのみサポートします。クエリは、ステートメントで構成されます。ステートメントのオブジェクトで使用される「attributeName」は、レターインスタンスオブジェクト内のプロパティの名前です。<br /> </td>
  </tr>
 </tbody>
</table>

#### 例 1：送信済みタイプのすべてのレターインスタンスを取得する {#example-fetch-all-the-letter-instances-of-type-submitted}

以下のコードで送信済みのレターインスタンスの一覧が返されます。ドラフトのみを取得するには、`LetterInstanceType.COMPLETE.name()`を`LetterInstanceType.DRAFT.name().`に変更します

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 例 2：特定のユーザーによって送信されたドラフトタイプのすべてのレターインスタンスを取得する {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下のコードでは、同一のクエリに複数のステートメントが含まれ、特定のユーザーが送信したレターインスタンス（submittedby 属性）や letterInstanceType がドラフトであるなど、異なる条件に基づいて結果がフィルタリングされます。

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### getLetterInstance の使用 {#using-nbsp-getletterinstance}

特定のレターインスタンス ID で識別されるレターインスタンスを取得します。一致するインスタンス ID がない場合、`` null を返します。

**構文：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### LetterInstance の有無の確認 {#verifying-if-letterinstance-exist}

レターインスタンスが指定した名前で存在するかどうかを確認します。

**構文**： `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **パラメーター** | **説明** |
|---|---|
| letterInstanceName | 有無を確認するレターインスタンスの名前。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## レターインスタンスを開く {#opening-letter-instances}

レターインスタンスには、送信済みタイプまたはドラフトタイプがあります。両タイプのレターインスタンスを開くと、それぞれ異なる動作を示します。

* 送信済みのレターインスタンスの場合、レターインスタンスを示す PDF が開きます。サーバー上に残存する送信済みのレターインスタンスにも dataXML と処理された XDP が含まれ、それらを PDF/A の作成のようなケースの実行やカスタマイズに使用することができます。
* ドラフトのレターインスタンスの場合、「通信を作成」UI が正確に前回のドラフトが作成された時点の状態に再読み込みされます。

### ドラフトのレターインスタンスを開く {#opening-draft-letter-instance-nbsp}

CCR UI cmLetterInstanceId パラメーターをサポートしており、これを使ってレターを再読み込みできます。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>通信の再読み込み時に cmLetterId または cmLetterName/State/Version を指定する必要はありません。再読み込みされた通信に関するすべての詳細は、送信済みデータに既に含まれています。RandomNo はブラウザーのキャッシュの問題を避けるために使用されます。乱数としてタイムスタンプを使用できます。

### 送信済みのレターインスタンスを開く {#opening-submitted-letter-instance}

送信済み PDF は、次のレターインスタンス ID を使用して直接開くことができます。

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
