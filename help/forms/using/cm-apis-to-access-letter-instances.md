---
title: レターインスタンスにアクセスするための API
seo-title: レターインスタンスにアクセスするための API
description: レターインスタンスにアクセスするための API を使用する方法について説明します。
seo-description: レターインスタンスにアクセスするための API を使用する方法について説明します。
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 57%

---


# レターインスタンスにアクセスするための API {#apis-to-access-letter-instances}

## 概要 {#overview}

Correspondence Management の「通信を作成」UI を使用して、作成中のレターインスタンスのドラフトを保存することができます。また、この UI には送信済みのレターインスタンスが存在します。

Correspondence Management には、送信済みまたはドラフトのレターインスタンスを取り扱うための一覧表示インターフェイスを構築できる API が用意されています。APIリストが開き、エージェントの送信済みおよびドラフトのレターインスタンスが開きます。これにより、エージェントはドラフトまたは送信済みのレターインスタンスで作業を続行できます。

## レターインスタンスの取得 {#fetching-letter-instances}

Correspondence Management は API を使用して、LetterInstanceService サービスからレターインスタンスを取得します。

| メソッド | 説明 |
|--- |--- |
| getAllLetterInstances | 入力クエリーパラメーターに基づいてレターインスタンスを取得します。 すべてのレターインスタンスを取得するには、クエリパラメーターをヌルとして渡します。 |
| getLetterInstance | レターインスタンス ID に基づいて指定したレターインスタンスを取得します。 |
| letterInstanceExists | LetterInstance が指定した名前で存在するかどうかをチェックします。 |

>[!NOTE]
>
>LetterInstanceServiceはOSGIサービスであり、そのインスタンスはJavaで@Referenceを使用して取得できます
>Class or sling.getService(LetterInstanceService. クラス)をJSPで使用します。

### getAllLetterInstances の使用 {#using-nbsp-getallletterinstances}

下記の API は、クエリオブジェクトに基づいてレターインスタンスを検索します（送信済みとドラフトの両方）。クエリオブジェクトがnullの場合、すべてのレターインスタンスを返します。 This API returns list of [LetterInstanceVO](https://helpx.adobe.com/experience-manager/6-2/forms/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) objects, which can be used for extracting additional information of letter instance

**構文**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>query パラメーターは、レターインスタンスの検索またはフィルタリングに使用されます。ここでのクエリは、オブジェクトの最上位の属性/プロパティのみをサポートします。 クエリは、ステートメントで構成されます。ステートメントのオブジェクトで使用される「attributeName」は、レターインスタンスオブジェクト内のプロパティの名前です。<br /> </td>
  </tr>
 </tbody>
</table>

#### 例 1：送信済みタイプのすべてのレターインスタンスを取得する {#example-fetch-all-the-letter-instances-of-type-submitted}

以下のコードで送信済みのレターインスタンスの一覧が返されます。To get only drafts, change the `LetterInstanceType.COMPLETE.name()` to `LetterInstanceType.DRAFT.name().`

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

次のコードは、同じクエリ内に複数のステートメントを持ち、1人のユーザーによって送信されたレターインスタンス（submittedby属性）やletterInstanceTypeのタイプがドラフトであるなど、異なる条件に基づいて結果をフィルタリングします。

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

特定のレターインスタンス ID で識別されるレターインスタンスを取得します。一致するインスタンスIDがない場合は「null」を返します。

**構文：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### レターインスタンスの有無の確認 {#verifying-if-letterinstance-exist}

レターインスタンスが指定した名前で存在するかどうかを確認します

**構文**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

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
* ドラフトのレターインスタンスの場合、「通信を作成」UIが、ドラフトが作成された時点の正確な前の状態に再読み込みされます。

### Opening Draft Letter Instance  {#opening-draft-letter-instance-nbsp}

CCR UIは、再読み込みされたレターに使用できるcmLetterInstanceIdパラメーターをサポートします。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>通信の再読み込み時にcmLetterIdまたはcmLetterName/State/Versionを指定する必要はありません。再読み込みされた通信に関するすべての詳細が、送信済みデータに既に含まれているためです。 RandomNoは、ブラウザーのキャッシュの問題を回避するために使用します。タイムスタンプを乱数として使用できます。

### 送信済みのレターインスタンスを開く {#opening-submitted-letter-instance}

送信済み PDF は、次のレターインスタンス ID を使用して直接開くことができます。

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
