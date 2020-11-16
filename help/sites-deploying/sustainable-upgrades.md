---
title: 持続可能なアップグレード
seo-title: 持続可能なアップグレード
description: AEM 6.4 の持続可能なアップグレードについて説明します。
seo-description: AEM 6.4 の持続可能なアップグレードについて説明します。
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 76%

---


# 持続可能なアップグレード{#sustainable-upgrades}

## カスタマイズフレームワーク {#customization-framework}

### Architecture (Functional / Infrastructure / Content / Application)  {#architecture-functional-infrastructure-content-application}

カスタマイズフレームワーク機能は、アップグレードしづらいコード（APIS など）またはコンテンツ（オーバーレイなど）などの拡張できない領域での違反が減少するように設計されています。

カスタマイズフレームワークには、**API サーフェス**&#x200B;と&#x200B;**コンテンツ分類**&#x200B;の 2 つのコンポーネントがあります。

#### API サーフェス {#api-surface}

AEM の以前のリリースでは、多くの API が Uber Jar を介して公開されていました。これらの API の一部は、お客様による使用を意図して公開されたものではなく、複数のバンドルにまたがって AEM 機能をサポートするために公開されたものです。今後は、アップグレードの観点からどの API が安全に使用できるかをお客様に示すために、Java API は、公開または非公開としてマークされます。その他の詳細を次に示します。

* Java APIs marked as `Public` can be used and referenced by custom implementation bundles.

* 公開 API は、互換パッケージのインストールによる後方互換性があります。
* 互換パッケージには、後方互換性を確保するために互換 Uber JAR が含まれます。
* Java APIs marked as `Private` are intended to only be used by AEM internal bundles and should not be used by custom bundles.

>[!NOTE]
>
>このコンテキストでの`Private`非公開および`Public`公開の概念を、Java の クラスおよび クラスの概念と混同しないようにしてください。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### コンテンツ分類 {#content-classifications}

AEM では、以前からオーバーレイの原理と Sling Resource Merger を使用して、ユーザーが AEM の機能の拡張およびカスタマイズをおこなうことができるようになっています。AEM コンソールと UI を強化する事前定義済みの機能は、**/libs** に格納されます。ユーザーは **/libs** の下は何も変更できませんが、**/apps** の下にコンテンツを追加して、**/libs** 内で定義されている機能をオーバーレイおよび拡張できます（詳しくは、「オーバーレイを使用した開発」を参照）。この場合も、AEM のアップグレード時に多数の問題が発生します。**/libs** 内のコンテンツが変更され、オーバーレイ機能が予期しない動作で破損することがあるからです。ユーザーは、`sling:resourceSuperType` を介した継承によって、または sling:resourceType を使用して **/libs** 内のコンポーネントを直接参照することによって、AEM コンポーネントを拡張することもできます。同様のアップグレードの問題は、参照およびオーバーライドの使用例で発生する可能性があります。

安全に使用およびオーバーレイできる **/libs** の領域を容易に理解してより安全になるように、**/libs** 内のコンテンツは次の mixin によって分類されています。

* **公開（granite:PublicArea）** - オーバーレイ、継承（`sling:resourceSuperType`）または直接使用（`sling:resourceType`）できるように、ノードを公開として定義します。公開としてマークされた /libs の下のノードは、互換パッケージを追加することで、アップグレードしても安全になります。通常、顧客は公開としてマークされたノードのみを利用する必要があります。

* **抽象（granite:AbstractArea）** - ノードを抽象として定義します。Nodes can be overlaid or inherited ( `sling:resourceSupertype`) but must not be used directly ( `sling:resourceType`).

* **最終（granite:FinalArea）** - ノードを最終として定義します。最終的な理想的に分類されるノードは、オーバーレイまたは継承しないでください。 Final nodes can be used directly via `sling:resourceType`. 最終ノードの下のサブノードは、デフォルトで内部と見なされます。

* ***Internal (granite:InternalArea)*** *- *ノードをinternalと定義します。 内部として分類されたノードは、オーバーレイ、継承、直接使用しないのが理想的です。これらのノードは、AEM の内部機能でのみ使用されます。

* **注釈なし** - ノードはツリー階層に基づいて分類を継承します。/ root はデフォルトで公開です。**親が内部または最終として分類されているノードも、内部として扱われます。**

>[!NOTE]
>
>これらのポリシーは、Sling 検索パスに基づくメカニズムに対してのみ適用されます。Other areas of **/libs** like a client-side library may be marked as `Internal`, but could still be used with standard clientlib inclusion. このような場合は、お客様が引き続き内部分類に従うことが重要です。

#### CRXDE Lite コンテンツタイプインジケーター {#crxde-lite-content-type-indicators}

Mixins applied in CRXDE Lite will show content nodes and trees that are marked as `INTERNAL` as being greyed out. For `FINAL` only the icon is greyed out. これらのノードの子もグレー表示されます。どちらの場合も、オーバーレイノード機能は無効になります。

**公開**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最終**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**コンテンツヘルスチェック**

>[!NOTE]
>
>AEM 6.5以降では、Adobeではコンテンツアクセス違反の検出にパターンディテクターを使用することを推奨します。 パターンディテクターレポートは、より詳細な情報を提供し、より多くの問題を検出して、偽陽性の発生確率を下げます。
>
>詳しくは、「パターン検出器によるアップグレードの複雑さの [評価](/help/sites-deploying/pattern-detector.md)」を参照してください。

AEM 6.5 にはヘルスチェックが付属しています。オーバーレイまたは参照されたコンテンツがコンテンツ分類と一致しない方法で使用された場合は、このヘルスチェックにより警告が表示されます。

** Sling/Granite Content Access Check**は、リポジトリを監視する新しいヘルスチェックで、顧客コードがAEMの保護ノードに不正にアクセスしているかどうかを確認します。

このヘルスチェックは **/apps** をスキャンし、通常は完了するまで数秒かかります。

この新しいヘルスチェックにアクセスするには、次の手順に従います。

1. AEM ホーム画面から、**ツール／運営／ヘルスレポート**&#x200B;に移動します。
1. 次に示すように、**Sling／Granite コンテンツアクセスチェック**&#x200B;をクリックします。

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

スキャンが完了すると、警告のリストが表示され、誤って参照されている保護されたノードをエンドユーザーに通知します。

![screenshot-2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

違反を修正すると、緑の状態に戻ります。

![screenshot-2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

ヘルスチェックには、バックグラウンドサービスによって収集された情報が表示されます。バックグラウンドサービスでは、オーバーレイまたはリソースタイプがすべての Sling 検索パスにわたって使用される場合は常に、非同期的にチェックが実行されます。コンテンツ mixin が誤って使用された場合、違反が報告されます。
