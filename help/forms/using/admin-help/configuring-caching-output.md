---
title: Output のキャッシュの構成
description: Output サービスはフォームデザイン、フラグメントおよび画像をキャッシュします。Output のキャッシュの設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1454'
ht-degree: 100%

---

# Output のキャッシュの構成  {#configuring-caching-for-output}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Output サービスは、XML フォームデータを、Designer で作成されたフォームデザインにマージして、様々な形式でドキュメント出力ストリームを作成します。

管理コンソールの Output ページには、Output サービスがアイテムをキャッシュする方法を制御する設定が含まれています。これらの設定を調整し、Output サービスのパフォーマンスを最適化できます。

Output サービスは、次のアイテムをキャッシュします。

* **フォームデザイン：** Output サービスは、リポジトリまたは HTTP ソースから取得したフォームデザインをキャッシュします。このキャッシュにより、以降のレンダリング要求では、Output サービスはリポジトリではなくキャッシュからフォームデザインを取得するようになり、パフォーマンスが向上します。
* **フラグメントおよび画像：** Output サービスは、フォームデザインで使用されるフラグメントと画像をキャッシュできます。Output サービスがこれらのオブジェクトをキャッシュすると、フラグメントと画像がリポジトリから読み取られるのは初回リクエスト時のみになるので、パフォーマンスが向上します。

Output では、次の 2 つの場所にキャッシュが格納されます。

* **メモリ内：**&#x200B;すばやくアクセスできるように、メモリ内にアイテムが格納されます。メモリ内キャッシュはサイズに制限があり、サーバーを再起動すると削除されます。
* **ディスク上：**&#x200B;サーバーのファイルシステムにアイテムが格納されます。ディスクキャッシュはメモリ内キャッシュよりも容量が大きく、サーバーを再起動しても保持されます。ディスクキャッシュの場所はアプリケーションサーバーによって異なります。ディスクキャッシュの場所の変更について詳しくは、[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照してください。

## キャッシュモードの指定 {#specifying-the-cache-mode}

Output では、次の 2 つのモードのキャッシュがサポートされています。

* 無条件
* キャッシュのチェックポイントの使用

キャッシュモード間を切り替える場合、変更を有効にするには、Output サービスを再起動します。このサービスを再起動するには、Workbench を使用するか、[AEM Forms モジュール関連サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)の説明を参照してください。

キャッシュのチェックポイント時間は、モードを切り替えるときに自動的にリセットされます。

### 無条件キャッシュの使用 {#using-unconditional-caching}

このモードでは、Output サービスはリクエストを受け取るときに、必要なリソース（フォームデザインおよびフラグメントや画像などの関連アセット）を検証します。この Output サービスは、リポジトリ内のリソースのタイムスタンプとキャッシュ内のリソースのタイムスタンプを比較します。キャッシュ内のリソースの方が古い場合は、Output サービスはそのリソースを更新します。

このキャッシュモードでは、必ず最新のリソースが使用されますが、Output サービスはキャッシュされた項目をリクエストごとにリポジトリに対して検証するので、パフォーマンスに影響します。このキャッシュモードは、リソースが頻繁に更新され、パフォーマンスを重要視しない開発およびステージング環境に適しています。

**無条件キャッシュの指定**

1. 管理コンソールで、サービス／Output をクリックします。
1. 「出力キャッシュコントロールの設定」で「無条件」を選択し、「保存」をクリックします。

### キャッシュのチェックポイントを使用する {#use-the-cache-check-point}

このモードでは、Output サービスは、キャッシュされたリソースのタイムスタンプがキャッシュのチェックポイント時間よりも古い場合にのみ、リポジトリで新しいバージョンのリソースを確認します。最新のキャッシュのチェックポイント時間は、管理コンソールの Output ページに表示されます。

このキャッシュモードは、パフォーマンスが重視され、リソースに対する変更が頻繁に行われない、高パフォーマンスの実稼動環境で使用します。キャッシュのチェックポイント時間は、リポジトリリソースに対する変更をデプロイするときにリセットできます。

**キャッシュのチェックポイント使用の指定**

1. 管理コンソールで、サービス／Output をクリックします。
1. 「出力キャッシュコントロールの設定」で、「最後の検証がキャッシュのチェックポイント時間よりも前に行われた場合」を選択し、「保存」をクリックします。

**キャッシュのチェックポイントのリセット**

1. 管理コンソールで、サービス／Output をクリックします。
1. 「出力キャッシュコントロールの設定」で、「キャッシュチェックポイント」をクリックします。

### キャッシュの内容のリセット {#reset-the-cache-contents}

キャッシュの内容はいつでもクリアできます。キャッシュをリセットすると、Output サービスは完全なレンダリングを実行し、新しいキャッシュを作成するので、各フォームでの初回リクエスト時の速度が低下します。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「出力キャッシュコントロールの設定」で、「キャッシュをリセット」をクリックします。

## キャッシュ設定の指定 {#configuring-cache-settings}

Output でキャッシュを使用するように設定を指定できます。こうすることにより、お使いの AEM Forms 環境のパフォーマンスを最適化することができます。

これらの設定にアクセスするには、管理コンソールで、サービス／Output をクリックします。

>[!NOTE]
>
>キャッシュのディスク要件は、リポジトリと同じである必要があります。

### グローバルキャッシュ設定の指定 {#specifying-global-cache-settings}

「**グローバルキャッシュ設定**」領域の設定は、すべての種類のキャッシュに影響します。これらの設定のいずれかを変更する場合、その変更を有効にするには、Output サービスを再起動します。このサービスを再起動するには、Workbench を使用するか、[AEM Forms モジュール関連サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)の説明を参照してください。

**最大キャッシュドキュメントサイズ（KB）：**&#x200B;任意のメモリ内キャッシュに保存できるフォームデザインまたはその他のリソースの最大サイズ（キロバイト単位）です。これはすべてのメモリ内キャッシュに適用されるグローバル設定です。リソースのサイズがこの値よりも大きい場合、そのリソースはメモリにキャッシュされません。デフォルト値は 1024 キロバイトです。この設定は、ディスクキャッシュには影響しません。

**フォームレンダリングキャッシュが有効です：**&#x200B;デフォルトでは、このオプションが選択されており、レンダリングされたフォームが以降の取得のためにキャッシュされます。この設定では、非インタラクティブドキュメントがキャッシュされないので、Output サービスのパフォーマンスにはほとんど影響がありません。このオプションは、クライアント上でレンダリングされている非インタラクティブドキュメントで Output サービスを使用しているときに効果を発揮します。

### フォームデザインをキャッシュ {#caching-form-designs}

Output サービスはレンダリングリクエストを受け取ると、リポジトリまたは HTTP ソースからフォームデザインを取得してキャッシュします。このキャッシュにより、以降のレンダリング要求では、Output サービスはリポジトリではなくキャッシュからフォームデザインを取得するようになり、パフォーマンスが向上します。

Output サービスは、常にフォームデザインをディスク上にキャッシュします。フォームデザインがサーバー上に格納されている場合、これらのファイルはディスクキャッシュと見なされます。また、Output サービスは、「**メモリ内テンプレートキャッシュ**」領域の設定に従って、フォームデザインをメモリ内にもキャッシュします。これらの設定のいずれかを変更する場合、その変更を有効にするには、Output サービスを再起動します。このサービスを再起動するには、Workbench を使用するか、[AEM Forms モジュール関連サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules)の説明を参照してください。

**テンプレート設定キャッシュサイズ：**&#x200B;メモリに保持するテンプレート設定オブジェクトの最大数です。デフォルト値は 100 です。この値は、テンプレートキャッシュサイズの値と同じかそれ以上の値に設定することをお勧めします。この設定は、ディスクキャッシュには影響しません。

**テンプレートキャッシュサイズ：**&#x200B;メモリ内に保持するテンプレートコンテンツオブジェクトの最大数です。デフォルト値は 100 です。この設定は、ディスクキャッシュには影響しません。

**有効：**&#x200B;デフォルトでは、このチェックボックスが選択されており、フォームテンプレートがメモリ内にキャッシュされます。このオプションが選択されていない場合、フォームテンプレートはディスク上にのみキャッシュされます。

### フラグメントと画像のキャッシュ {#caching-fragments-and-images}

Output サービスは、フォームデザインで使用されるフラグメントと画像をディスク上にキャッシュします。これにより、フラグメントと画像がリポジトリから読み取られるのは初回リクエスト時のみになるので、パフォーマンスが向上します。以降のリクエストでは、Output サービスは、ディスクキャッシュからフラグメントおよび画像を読み取ります。フラグメントと画像はディスク上にのみキャッシュされます。メモリ内にはキャッシュされません。

ディスク上でのフラグメントおよび画像のキャッシュを制御するには、次の設定を使用します。これらの設定は、「**テンプレートリソースキャッシュ設定**」領域にあります。

**リソースのキャッシュ**&#x200B;リストから次のいずれかのオプションを選択します。

**フラグメントと画像に対して有効にする：** Output サービスはフラグメントと画像をキャッシュします。これはデフォルトのオプションです。

**フラグメントに対して有効にする：** Output サービスはフラグメントをキャッシュしますが、画像はキャッシュしません。

**無効：** Output サービスは、フラグメントも画像もキャッシュしません。

**クリーンアップの間隔（秒単位）：** Output サービスで無効な古いキャッシュファイルを削除する頻度を指定します。Output サービスでは、有効なキャッシュファイルは削除されません。クリーンアップの間隔を変更する場合、その変更を有効にするには、Output サービスを再起動します。このサービスを再起動するには、Workbench を使用するか、AEM Forms モジュール関連サービスの開始と停止の説明を参照してください。

## クラスター環境のキャッシュに関する考慮事項 {#clustering-considerations-for-caches}

クラスター環境では、ノードごとに独自のメモリ内キャッシュとディスクキャッシュが保持されます。各ノードのキャッシュ内容は、そのノードでレンダリングされているフォームによって異なります。

キャッシュの場所は、クラスターの各ノードで同一（同じディスクおよびパス）である必要があります。共有ストレージにはキャッシュを置かないでください。

管理コンソールの Output ページを使用して特定のノードのキャッシュ設定を変更すると、そのノードでリクエストを受け取るときに、他のノードのキャッシュ設定が更新されます。この動作は、「キャッシュをリセット」ボタンにも適用されます。あるノードの「キャッシュをリセット」ボタンをクリックすると、そのノードからは直ちにキャッシュが削除されます。他のノードのキャッシュについては、リクエストがそのノードに送信されるとクリアされます。
