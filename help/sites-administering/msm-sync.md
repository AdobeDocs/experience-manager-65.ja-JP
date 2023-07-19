---
title: ライブコピーの同期の設定
seo-title: Configuring Live Copy Synchronization
description: ライブコピーの同期の設定について説明します。
seo-description: Learn about configuring Live Copy Synchronization.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
feature: Multi Site Manager
exl-id: ac24b8b4-b3ed-47fa-9a73-03f0c9e68ac8
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 63%

---

# ライブコピーの同期の設定 {#configuring-live-copy-synchronization}

ライブコピーをソースコンテンツと同期する方法とタイミングを制御するには、次のタスクを実行します。

* 既存のロールアウト設定が要件を満たしているかどうか、または 1 つ以上のロールアウト設定を作成する必要があるかどうかを決定します。
* ライブコピーに使用するロールアウト設定を指定します。

## インストールされるロールアウト設定とカスタムロールアウト設定 {#installed-and-custom-rollout-configurations}

この節では、インストールしたロールアウト設定、それらの設定で使用する同期アクション、カスタム設定を作成する方法（必要な場合）について説明します。

>[!CAUTION]
>
>インストール済みの標準のロールアウト設定を、更新したり変更したりすることは **推奨しません**。カスタムのライブアクションが必要な場合は、カスタムロールアウトの設定で追加してください。

### ロールアウトトリガー {#rollout-triggers}

各ロールアウト設定は、ロールアウトトリガーを使用してロールアウトを発生させます。 ロールアウト設定では、次のいずれかのトリガーを使用できます。

* **ロールアウト時**：**ロールアウト**&#x200B;コマンドをブループリントページで使用します。または、**同期**&#x200B;コマンドをライブコピーページで使用します。

* **変更時**：ソースページが変更されます。

* **アクティベート時**：ソースページがアクティベートされます。

* **アクティベート解除時**：ソースページがアクティベート解除されます。

>[!NOTE]
>
>変更時トリガーを使用すると、パフォーマンスに影響を及ぼす可能性があります。詳しくは、[MSM のベストプラクティス](/help/sites-administering/msm-best-practices.md#onmodify)を参照してください。

### インストール済みのロールアウト設定 {#installed-rollout-configurations}

次の表に、AEMと共にインストールされるロールアウト設定を示します。 表には各ロールアウト設定のトリガーと同期アクションが含まれます。インストールされたロールアウト設定のアクションが要件を満たさない場合は、次の操作を実行できます。 [新しいロールアウト設定を作成](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>名前</th>
   <th>説明</th>
   <th>トリガー</th>
   <th>同期アクション<br /> <br /> 関連情報 <a href="#installed-synchronization-actions">インストール済みの同期アクション</a></th>
  </tr>
  <tr>
   <td>標準ロールアウト設定</td>
   <td>ロールアウトトリガーでロールアウトプロセスを開始するのを許可したり、アクション（コンテンツの作成、更新、削除や子ノードの整理）を実行したりする標準のロールアウト設定です。。</td>
   <td>ロールアウト時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>ブループリントのアクティベート時にアクティベート</td>
   <td>ソースが公開されたときにライブコピーを公開します。</td>
   <td>アクティベート時</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>ブループリントのアクティベート解除時にアクティベート解除</td>
   <td>ソースが非アクティブ化された場合に、ライブコピーを非アクティブ化します。</td>
   <td>アクティベート解除時</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>変更時にプッシュ</td>
   <td><p>ソースが変更された場合に、コンテンツをライブコピーにプッシュします。</p> <p>このロールアウト設定は、[ 変更時 ]トリガーを使用するので、慎重に使用してください。</p> </td>
   <td>変更時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>変更時にプッシュ（シャロー）</td>
   <td><p>参照を更新することなく、ブループリントページが変更されたときに、ライブコピーにコンテンツをプッシュします（シャローコピーの場合など）。</p> <p>このロールアウト設定は、[ 変更時 ]トリガーを使用するので、慎重に使用してください。</p> </td>
   <td>変更時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>ローンチを昇格</td>
   <td>ローンチページを昇格するための標準ロールアウト設定です。</td>
   <td>ロールアウト時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>カタログページコンテンツのロールアウト設定</td>
   <td>カタログのブループリントのページテンプレートを適用します。</td>
   <td>ロールアウト時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>カタログページ更新のロールアウト設定</td>
   <td>カタログのブループリントのターゲットプロパティを適用します。 カタログページコンテンツのロールアウト設定の後に実行する必要があります。</td>
   <td>ロールアウト時</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>DPS パブリケーションのロールアウト設定</td>
   <td>DPS パブリッシュのロールアウト設定。最初のロールアウトで FolioProducer バインディングプロパティを除外しながら、ロールアウトトリガーでロールアウトプロセスを開始できます。</td>
   <td>ロールアウト時</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>レガシー (5.6.0) カタログロールアウト設定</td>
   <td>非推奨です。カタログロールアウトには、MSM ではなく Catalog Generator を使用してください。</td>
   <td>ロールアウト時</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### インストール済みの同期アクション {#installed-synchronization-actions}

次のテーブルに、AEM と共にインストールされる同期アクションのリストを示します。インストールされているアクションが要件を満たさない場合は、[新しい同期アクションを作成](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)できます。

<table>
 <tbody>
  <tr>
   <th>アクション名</th>
   <th>説明</th>
   <th>プロパティ<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>ソースのノードがライブコピーに存在しない場合は、ライブコピーにノードをコピーします。<a href="#excluding-properties-and-node-types-from-synchronization">CQ MSM Content Copy Action サービスを設定</a>して、除外するノードタイプ、段落項目、ページプロパティを指定してください。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>ソースに存在しないライブコピーのノードを削除します。<a href="#excluding-properties-and-node-types-from-synchronization">CQ MSM Content Delete Action サービスを設定</a>して、除外するノードタイプ、段落項目およびページプロパティを指定してください。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>ソースからの変更を使用してライブコピーのコンテンツを更新します。<a href="#excluding-properties-and-node-types-from-synchronization">CQ MSM Content Update Action サービスを設定</a>して、除外するノードタイプ、段落項目、ページプロパティを指定してください。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>ライブコピーのプロパティを編集します。 editMap プロパティは、編集するプロパティとその値を決定します。 editMap プロパティの値は、次の形式を使用する必要があります。</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p><code>current_value</code> と <code>new_value</code> の項目は正規表現です。<br /> </p> <p>例えば、editMap の次の値を検討してください。</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>この値は、ライブコピーのノードのプロパティを次のように編集します。</p>
    <ul>
     <li><code>contentpage</code> または <code>homepage</code> のどちらかに設定されている <code>sling:resourceType</code> プロパティは次のように設定されます。 <code>mobilecontentpage.</code></li>
     <li><code>contentpage</code> に設定されている <code>cq:template</code> プロパティは次のように設定されます。 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap:(String) プロパティ、現在の値および新しい値を識別します。 詳しくは、説明を参照してください。<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>ページがロールアウトされたページイベントを送信します。 通知が送信されるようにするには、最初にロールアウトイベントを購読する必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>ライブコピーでは、ブループリント上の順序に基づいて子（ノード）を並べ替えます<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>この同期アクションにより、ライブコピーでは、リンクなどの参照が更新されます。<br />ブループリント内の特定のリソースを指す、ライブコピーページ内のパスを検索します。見つかると、パスが更新され、（ブループリントではなく）ライブコピー内の関連リソースを指すようになります。 ブループリント外のターゲットを持つ参照は変更されません。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">CQ MSM References Update Action サービスを設定</a>して、除外するノードタイプ、段落項目、ページプロパティを指定してください。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>ライブコピーのバージョンを作成します。</p> <p>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>ライブコピーをアクティベートします。</p> <p>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>ライブコピーを非アクティブ化します。</p> <p>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td><p>target プロパティで定義されているワークフローを開始し（ページの場合のみ）、ライブコピーをペイロードとして取ります。</p> <p>モデルノードのパスがターゲットパスになります。</p> </td>
   <td>ターゲット：(String) ワークフローモデルのパス。<br /> </td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td><p>ライブコピーページ上の複数の ACL の権限を、特定のユーザーグループに対して読み取り専用に設定します。 次の ACL が設定されています。</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>このアクションはページにのみ使用してください。</p> </td>
   <td>target：（文字列）権限を設定するグループの ID。<br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>ライブコピーページ上の複数の ACL の権限を、特定のユーザーグループに対して読み取り専用に設定します。 次の ACL が設定されています。</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>このアクションはページにのみ使用してください。</p> </td>
   <td>target：（文字列）権限を設定するグループの ID。 </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>ライブコピーページ上の ActionSet.ACTION_NAME_REMOVE ACL の権限を、特定のユーザーグループについて読み取り専用に設定します。このアクションはページにのみ使用してください。</td>
   <td>target：（文字列）権限を設定するグループの ID。 </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>ブループリント／ソースページが少なくとも 1 回公開された場合は、公開されたバージョンを使用してライブコピーページを作成します。メモ：このアクションは、公開されたソースページに基づくライブコピーページの作成でのみ使用できます。既存のライブコピーページの更新では使用できません。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>PageMoveAction は、ページがブループリント内で移動された場合に適用されます。</p> <p>アクションは、（関連する）LiveCopy ページを移動前の場所から移動後の場所に移動するのではなく、コピーします。</p> <p>PageMoveAction は、移動前の場所にある LiveCopy ページを変更しません。 したがって、連続する RolloutConfigurations の場合、ブループリントのない LiveRelationship のステータスになります。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">CQ MSM Page Move Action サービスを設定</a>して、除外するノードタイプ、段落項目およびページプロパティを指定してください。 </p> <p>このアクションは、ロールアウト設定に含まれる唯一の同期アクションである必要があります。</p> </td>
   <td><p>prop_referenceUpdate:（ブール値）参照を更新するには、true に設定します。 デフォルトは true です。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>カタログ内の製品リソースを作成または更新します。 このアクションは、次のいずれかの状況で使用することを目的としています。
    <ul>
     <li>カタログ（またはカタログセクション）の生成またはロールアウト</li>
     <li>ユーザは、製品コンポーネントの同期継承を復元します。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>ローンチが作成したコンテンツにライブ関係が存在することを示します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>カタログ生成固有のロールアウトフックを実行します。 CatalogGenerator の executePageRolloutHooks メソッドと executeProductRolloutHooks メソッドを呼び出します。<br /> AEM Javadoc のcom.adobe.cq.commerce.pim.api.CatalogGenerator を参照してください。</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>製品カタログのライブコピーの製品ページを更新します</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### ロールアウト設定の作成 {#creating-a-rollout-configuration}

以下が可能です。 [ロールアウト設定の作成](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) インストールされたロールアウト設定がアプリケーションの要件を満たさない場合：

* [ロールアウト設定を作成します](/help/sites-developing/extending-msm.md#create-the-rollout-configuration)。
* [ロールアウト設定に同期アクションを追加します](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration)。

ブループリントページまたはライブコピーページでロールアウト設定を指定すると、新しいロールアウト設定を使用できるようになります。

### プロパティとノードタイプの同期からの除外 {#excluding-properties-and-node-types-from-synchronization}

対応する同期アクションをサポートする複数の OSGi サービスを設定して、特定のノードタイプやプロパティに影響を与えないようにすることができます。例えば、AEM の内部機能に関連する多くのプロパティとサブノードをライブコピーに含めることはできません。コピーする必要があるのは、ページのユーザーに関連するコンテンツだけです。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

次の表に、除外するノードを指定できる同期アクションを示します。 この表には、Web コンソールを使用して設定する場合のサービスの名前とリポジトリーノードを使用して設定する場合の PID が示されています。

| 同期アクション | Web コンソールのサービス名 | サービス PID |
|---|---|---|
| contentCopy | CQ MSM Content Copy Action | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | CQ MSM Content Delete Action | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | CQ MSM Content Update Action | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | CQ MSM Page Move Action | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | CQ MSM References Update Action | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

次の表は、設定可能なプロパティを示しています。

<table>
 <tbody>
  <tr>
   <th>Web コンソールのプロパティ/ OSGi プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><p>除外されたノードタイプ</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>同期アクションから除外するノードタイプに一致する正規表現。</td>
  </tr>
  <tr>
   <td><p>Excluded Paragraph Items</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>同期アクションから除外する段落項目に一致する正規表現。</td>
  </tr>
  <tr>
   <td><p>Excluded Page Properties</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>同期アクションから除外するページプロパティに一致する正規表現。</td>
  </tr>
  <tr>
   <td><p>Ignored Mixin NodeTypes</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>CQ MSM Content Update Action でのみ使用できます。同期アクションから除外する mixin ノードタイプの名前に一致する正規表現です。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>クラシック UI では、ライブコピーページのページプロパティダイアログボックスに表示されるロックアイコンに、 Excluded Page Properties プロパティの設定が反映されていません。 ロックアイコンは、同期アクションから除外されたプロパティに対しても表示されます。

>[!NOTE]
>
>タッチ操作向け UI の場合は、[ページプロパティの MSM ロックの設定（タッチ操作向け UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui)も参照してください。

#### CQ MSM Content Update Action - 除外 {#cq-msm-content-update-action-exclusions}

いくつかのプロパティとノードタイプは、デフォルトで除外されます。これらは、の OSGi 設定で定義されます。 **CQ MSM Content Update Action**&#x200B;の下 **除外されたページのプロパティ**.

デフォルトでは、次の正規表現に一致するプロパティは、ロールアウト時に除外されます（つまり、更新されません）。

![CQ MSM Content Update Action](assets/chlimage_1.png)

必要に応じて、除外リストを定義する表現を変更できます。

例えば、ロールアウトで考慮される変更にページ&#x200B;**タイトル**&#x200B;を含めるには、除外から `jcr:title` を削除します。正規表現は次のようになります。

`jcr:(?!(title)$).*`

### 参照を更新するための同期の設定 {#configuring-synchronization-for-updating-references}

参照の更新に関連する、対応する同期アクションをサポートする複数の OSGi サービスを設定できます。

AEM を操作する際は、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

次の表に、参照の更新を指定できる同期アクションを示します。 この表には、Web コンソールを使用して設定する場合のサービスの名前とリポジトリーノードを使用して設定する場合の PID が示されています。

<table>
 <tbody>
  <tr>
   <th>Web コンソールのプロパティ/ OSGi プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><p>ネストされたライブコピーの参照を更新</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>CQ MSM References Update Action でのみ使用できます。 最上位のライブコピーのブランチ内にあるリソースをターゲットとする参照を置き換えるには、このオプションを選択する（Web コンソール）か、この boolean プロパティを true に設定します（リポジトリ設定）。</td>
  </tr>
  <tr>
   <td><p>Update Referencing Pages</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>CQ MSM Page Move Action でのみ使用できます。元のページを使用する参照を、ライブコピーページを参照するように更新するには、このオプションを選択する（Web コンソール）か、この boolean プロパティを <code>true</code> に設定します（リポジトリ設定）。</td>
  </tr>
 </tbody>
</table>

## 使用するロールアウト設定の指定 {#specifying-the-rollout-configurations-to-use}

MSM を使用すると、通常使用するロールアウト設定のセットを指定できます。必要に応じて、特定のライブコピー用にロールアウト設定を上書きすることもできます。MSM では、使用するロールアウト設定を複数の場所で指定できます。この場所では、特定のライブコピーに設定を適用するかどうかを指定します。

使用するロールアウト設定を指定できる場所を以下に示します。また、ライブコピーに使用するロールアウト設定を MSM がどのように決定するかについても説明します。

* **[ライブコピーページのプロパティ](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page)：** 1 つ以上のロールアウト設定を使用するようにライブコピーページが設定される場合、MSM ではそれらのロールアウト設定を使用します。
* **[ブループリントページのプロパティ](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page)：**&#x200B;ライブコピーがブループリントに基づいており、ライブコピーページがロールアウト設定を使用して設定されない場合は、ブループリントのソースページに関連付けられているロールアウト設定が使用されます。
* **ライブコピーの親ページプロパティ：**&#x200B;ライブコピーページもブループリントのソースページもロールアウト設定を使用して設定されない場合は、ライブコピーページの親ページに適用されるロールアウト設定が使用されます。
* **[システムのデフォルト](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)：**&#x200B;ライブコピーの親ページのロールアウト設定を特定できない場合は、システムのデフォルトのロールアウト設定が使用されます。

例えば、ブループリントでは We.Retail 参照サイトをソースコンテンツとして使用します。 ブループリントからサイトが作成されます。 次のリストの各項目では、ロールアウト設定の使用に関する様々なシナリオについて説明します。

* どのブループリントページまたはライブコピーページもロールアウト設定を使用するように設定されていない場合、MSM では、システムのデフォルトのロールアウト設定をすべてのライブコピーページに使用します。
* We.Retail 参照サイトのルートページは、複数のロールアウト設定を使用して設定されます。 この場合、MSM では、これらのロールアウト設定をすべてのライブコピーページに使用します。
* We.Retail 参照サイトのルートページが複数のロールアウト設定を使用して設定されており、ライブコピーサイトのルートページが別のロールアウト設定のセットを使用して設定されている。MSM では、ライブコピーサイトのルートページで設定されたロールアウト設定を使用します。

### ライブコピーページ用のロールアウト設定の指定 {#setting-the-rollout-configurations-for-a-live-copy-page}

ソースページがロールアウトされる際に使用するロールアウト設定を使用してライブコピーページを設定します。 デフォルトでは、子ページは設定を継承します。使用するロールアウト設定を指定する場合は、ライブコピーページがその親から継承する設定を上書きします。

[ライブコピーの作成](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)時に、ライブコピーページ用のロールアウト設定を指定することもできます。

1. **Sites** コンソールを使用してライブコピーページを選択します。
1. ツールバーの「**プロパティ**」を選択します。
1. 「**ライブコピー**」タブを開きます。

   「**設定**」セクションには、ページが継承するロールアウト設定が表示されます。

   ![設定](assets/chlimage_1-1.png)

1. 必要に応じて、「**ライブコピーの継承**」フラグを変更します。オンにした場合、ライブコピー設定がすべての子で有効になります。

1. をクリア **ロールアウト設定を親から継承** プロパティを選択し、リストから 1 つ以上のロールアウト設定を選択します。

   選択したロールアウト設定がドロップダウンリストの下に表示されます。

   ![選択したロールアウト設定](assets/chlimage_1-2.png)

1. 「**保存**」をクリックまたはタップします。

### ブループリントページ用のロールアウト設定の指定 {#setting-the-rollout-configuration-for-a-blueprint-page}

ブループリントページがロールアウトされる際に使用するロールアウト設定を含むブループリントページを設定します。

ブループリントページの子ページは設定を継承します。 使用するロールアウト設定を設定する際に、ページが親から継承する設定を上書きできます。

1. **サイト**&#x200B;コンソールを使用してブループリントのルートページを選択します。
1. ツールバーの「**プロパティ**」を選択します。
1. 「**ブループリント**」タブを開きます。
1. ドロップダウンセレクターを使用して&#x200B;**ロールアウト設定**&#x200B;を 1 つ以上選択します。
1. 「**保存**」を選択して更新内容を保持します。

### システムのデフォルトのロールアウト設定の指定 {#setting-the-system-default-rollout-configuration}

システムの既定値として使用するロールアウト設定を指定します。 デフォルトを指定するには、OSGi サービスを設定します。

* **Day CQ WCM Live Relationship Manager**
サービス PID は `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

このサービスを設定するには、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または[リポジトリノード](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を使用します。

* Web コンソールの場合、設定するプロパティの名前は Default rollout config です。
* リポジトリーノードを使用する場合、設定するプロパティの名前は `liverelationshipmgr.relationsconfig.default` です。

このプロパティの値を、システムのデフォルトとして使用するロールアウト設定のパスに指定します。デフォルト値は `/libs/msm/wcm/rolloutconfigs/default` です。これは&#x200B;**標準のロールアウト設定**&#x200B;です。
