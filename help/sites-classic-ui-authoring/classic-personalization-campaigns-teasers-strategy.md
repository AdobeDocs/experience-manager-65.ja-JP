---
title: ティーザーと戦略
description: キャンペーンでは多くの場合、訪問者の特定のセグメントの関心を引き、その関心事項に焦点を当てたコンテンツに誘導するためのメカニズムとして、ティーザーを使用します。特定のキャンペーンに対して 1 つ以上のティーザーが定義されています。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 100%

---

# ティーザーと戦略 {#teasers-and-strategies}

キャンペーンでは多くの場合、訪問者の特定のセグメントの関心を引き、その関心事項に焦点を当てたコンテンツに誘導するためのメカニズムとして、ティーザーを使用します。特定のキャンペーンに対して 1 つ以上のティーザーが定義されています。

>[!NOTE]
>
>ティーザーコンポーネントは、AEM 6.2 で非推奨（廃止予定）となりました。代わりに、[ターゲットコンポーネント](/help/sites-authoring/content-targeting-touch.md)を使用してください。

* **ブランドページ**&#x200B;は、web サイトの「キャンペーン」セクションに格納されます。各ブランドには個々のキャンペーンが含まれます。
* **キャンペーンページ**&#x200B;は、web サイトの「キャンペーン」セクションに格納されます。各キャンペーンには個々のページがあり、ページの下にティーザー定義が保持されます。コンテナページまたは概要ページにも、個々のティーザーページに関する特定の情報と統計情報が保持されます。

AEM 内のティーザーは、次の複数の部分で構成されています。

* **ティーザーページ**&#x200B;は各キャンペーンページに格納され、各キャンペーンにのみ使用できるティーザー段落の定義を保持します。これらの定義は、ティーザー段落を表示する際に使用されます。コンテンツのバリエーション、バリエーションとブースト係数の選択に使用されるセグメントなどがあります。
* **ティーザーコンポーネント**&#x200B;は標準提供ですぐに使用でき、コンテンツページに特定のティーザー段落のインスタンスを作成できます。サイドキックからティーザーコンポーネントをドラッグし、ティーザー定義を指定して独自のティーザー段落を作成できます。**メモ：**&#x200B;ティーザーコンポーネントは AEM 6.2 で非推奨（廃止予定）となりました。代わりに[ターゲットコンポーネント](/help/sites-authoring/content-targeting-touch.md)を使用してください。
* **ティーザー段落**&#x200B;は、コンテンツページ内のティーザーの実際のインスタンスです。訪問者セグメントの一部を引き付けて、関心を持ったコンテンツに誘導します。
* 特定の訪問者セグメントに焦点を当てたキャンペーンコンテンツを保持するページ。通常、ティーザー段落は、訪問者をそのようなページに誘導します。

## 戦略 {#strategies}

ティーザー段落をページに追加する際に、**戦略**&#x200B;を定義する必要があります。

これは、割り当てられたセグメントがすべて正常に解決され、複数のティーザーを選択できる場合を想定しています。**戦略**&#x200B;では、表示されるティーザーの選択に使用する追加の条件を指定します。

* **Clickstream のスコア**&#x200B;は、訪問者のクライアントコンテキスト内に保持されるタグおよび関連するタグのヒットに基づきます（訪問者が各タグを含むページをクリックした頻度を示します）。ティーザーページに定義されている複数のタグのヒット率が比較されます。
* **ランダム**：「ランダム」に選択されます。ページ用に生成されたランダム係数を使用します。これは [Client Context](/help/sites-administering/client-context.md) で確認できます。
* **最初**：解決されたセグメントのリストの最初の項目を使用します。この順序は、キャンペーンコンテナページ内のティーザーの順序を指します。

セグメントの[ブースト計数](/help/sites-administering/campaign-segmentation.md#boost-factor)も選択に影響します。これは、セグメントの定義に追加される重み付け係数で、選択される相対的な確率を増減させます。

様々な選択条件のプロセスと相互関係をを示すには、例を使用するのが最も効果的です（この方法は、適切なオーディエンスにティーザーを確実に到達させるためにも使用できます）。

次のセグメントが既に作成され、それぞれにブースト係数が割り当てられている場合を考えます。

| セグメント | ブースト係数 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

次のティーザー定義を使用します。

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>ティーザー</td>
   <td>割り当てられたセグメント</td>
   <td>割り当てるタグ </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1、S2</td>
   <td>ビジネス、マーケティング</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>マーケティング</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>ビジネス<br /> </td>
  </tr>
 </tbody>
</table>

次に、これを以下の訪問者に適用します。

* **S1**、**S2 および **S6** が適切に解決された訪問者

* **マーケティング**&#x200B;タグに 3 回ヒットした訪問者
* **ビジネス**&#x200B;タグに 6 回ヒットした訪問者

結果は次のようになります。

* マッチング成功 - ティーザーに割り当てられたセグメントのいずれかが、現在の訪問者に対して正常に解決されますか。
* ブースト係数 - 適用可能なすべてのセグメントの中で最も高いブースト係数
* クリックストリームのスコア - 適用可能なすべてのタグヒットの累積合計

これらの値を次のように計算してから、適切な方法を適用します。

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>ティーザー</td>
   <td>割り当てられたセグメント</td>
   <td>タグ </td>
   <td>一致は成功するか</td>
   <td>結果のブースト係数</td>
   <td>結果のクリックストリームスコア </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1、S2</td>
   <td>ビジネス、マーケティング</td>
   <td>はい</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>はい</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
   <td>いいえ</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
   <td>はい<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>マーケティング</td>
   <td>はい</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>ビジネス</td>
   <td>はい</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

これらの値は、ティーザー段落に適用する&#x200B;**戦略**&#x200B;に応じて、訪問者に表示するティーザーを決定する際に使用されます。

<table>
 <tbody>
  <tr>
   <td>方法</td>
   <td>結果のティーザー</td>
   <td>コメント</td>
  </tr>
  <tr>
   <td>最初</td>
   <td>T5</td>
   <td>T5 と T6 のみが検討対象となります。これらのセグメントがすべて解決され、かつ、そのブースト係数が最大となるからです<i>。</i>リストは T5、T6 の順序で返されるので、T5 が選択されて表示されます。</td>
  </tr>
  <tr>
   <td>ランダム</td>
   <td>T5 または T6</td>
   <td>両方のティーザーに、すべてが解決され、同じブースト係数を持つセグメントがあります。そのため、2 つのティーザーが同じ比率として表示されます。</td>
  </tr>
  <tr>
   <td>クリックストリームのスコア</td>
   <td>T6</td>
   <td><p>T1、T4、T5、T6 のセグメントはすべてその訪問者に対して解決されます。T5 および T6 のブースト係数の方が高いので、T1 および T4 は除外されます。最後に T6 のクリックストリームスコアの方が高いので、T6 が選択されます。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>上記の解決テクニックの後に、複数のティーザーが選択可能な場合、内部選択（ランダム）により、1 つのティーザーが選択され、表示されます。
>
>例えば、戦略がクリックストリームのスコアで、T5 が T6 と同じクリックストリームのスコア（つまり、3 ではなく 6）の場合、内部選択（ランダム）を使用してこの 2 つの中から 1 つを選択します。

ティーザーページ／段落を使用して、特定の訪問者セグメントを、その訪問者の関心に基づきフォーカスされたコンテンツに誘導します。訪問者が選択できる様々なオプションを表示したり、特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示したりできます。例えば、訪問者の年齢によって異なるティーザー段落を表示できます。

通常、ティーザーページは、次のティーザーページに置き換えられるまで、一定の時間継続する一時的なアクションです。

ブランドとキャンペーンを作成した後、ティーザーエクスペリエンスを作成し、設定できます。

### ティーザーのタッチポイントの作成 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>ティーザーコンポーネントは AEM 6.2 で廃止されました。代わりに [Target コンポーネント](/help/sites-authoring/content-targeting-touch.md)を使用してください。

1. キャンペーンページに誘導するティーザー段落を配置するコンテンツページに移動します。
1. 必要な位置に&#x200B;**ティーザー**&#x200B;コンポーネント（サイドキックの「**パーソナライズ機能**」セクションで使用可能）を追加します。最初に作成したときには、キャンペーンパスがまだ設定されていないと表示されます。

   ![chlimage_1](assets/chlimage_1.png)

1. ティーザーコンポーネントを編集し、次の要素を追加します。

   * **キャンペーンパス**
個々のティーザーページが保存されるキャンペーンページへのパス。セグメントによって表示されるティーザーが決まります。

   * **[方法](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
適切に解決されたセグメントが複数ある場合の選択方法。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 「**OK**」をクリックして保存します。ティーザーに設定したセグメントや、現在ログインに使用しているユーザーのプロファイルに応じて、適切なコンテンツが表示されます。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. ティーザー段落にマウスオーバーすると、疑問符アイコンが（コンポーネントの右下隅に）表示されます。これをクリックすると、適用されるセグメントと、これらのセグメントが現在解決されているかが表示されます。

   ![chlimage_1-3](assets/chlimage_1-3.png)

### ティーザーの概要 {#teaser-overview}

MCM のキャンペーンビューと同様に、キャンペーンページには、そのページに接続されているティーザーに関する情報も表示されます。

1. **Web サイト**&#x200B;コンソールから、例えば次のようなキャンペーンページを開きます。

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   このページには、ティーザーの定義と閲覧の統計についての概要が表示されます。

   ![chlimage_1-4](assets/chlimage_1-4.png)
