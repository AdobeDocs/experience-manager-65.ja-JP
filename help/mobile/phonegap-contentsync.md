---
title: AEMとAdobe PhoneGap Enterprise のコンテンツ同期
description: このページでは、AEMを使用したAdobe PhoneGap Enterprise のコンテンツ同期について説明します。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '2975'
ht-degree: 0%

---

# モバイルとコンテンツ同期{#mobile-with-content-sync}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!NOTE]
>
>このドキュメントは、 [AEM Mobileの概要](/help/mobile/getting-started-aem-mobile.md) ガイド (AEM Mobileリファレンスの出発点として推奨 )。

コンテンツ同期を使用してコンテンツをパッケージ化し、ネイティブモバイルアプリケーションで使用できるようにします。 AEMで作成されたページは、デバイスがオフラインの場合でも、アプリコンテンツとして使用できます。 さらに、AEMページは Web 標準に基づいているので、クロスプラットフォームで機能し、任意のネイティブラッパーに埋め込むことができます。 この戦略により、開発の作業が軽減され、アプリコンテンツを簡単に更新できます。

>[!NOTE]
>
>AEMツールを使用して作成する PhoneGap アプリは、既にAEMページをコンテンツ同期経由でコンテンツとして使用するように設定されています。

コンテンツ同期フレームワークは、Web コンテンツを格納するアーカイブファイルを作成します。 単純なページ、画像、PDFファイル、Web アプリケーション全体から、あらゆるコンテンツを作成できます。 コンテンツ同期 API を使用すると、モバイルアプリまたはビルドプロセスからアーカイブファイルにアクセスして、コンテンツを取得してアプリに含めることができます。

次に、コンテンツ同期の一般的な使用例を示します。

1. AEM開発者は、含めるコンテンツを指定するコンテンツ同期設定を作成します。
1. コンテンツ同期フレームワークがコンテンツを収集し、キャッシュします。
1. モバイルデバイスでは、モバイルアプリケーションが起動され、サーバーからコンテンツを要求して、ZIP ファイルで配信されます。
1. クライアントは、ZIP コンテンツをローカルファイルシステムに展開します。 ZIP ファイル内のフォルダー構造は、クライアント（ブラウザーなど）が通常サーバーから要求するパスをシミュレートします。
1. クライアントは、埋め込みブラウザーでコンテンツを開くか、他の方法で使用します。
1. その後、クライアントは更新されたコンテンツをサーバーから要求します。 コンテンツ同期フレームワークは、ダウンロードサイズと時間を短縮するための増分的な更新を提供します。帯域幅やデータ量が制限されるので、モバイルデバイスにとって重要なこととなります。

>[!NOTE]
>
>コンテンツ同期ハンドラーの開発に関するガイドラインや、標準搭載のアプリハンドラーについて詳しくは、 [コンテンツ同期ハンドラーの開発](/help/mobile/contentsync-app-handlers.md).

## コンテンツ同期コンテンツの設定 {#configuring-the-content-sync-content}

コンテンツ同期設定を作成して、クライアントに配信される ZIP ファイルのコンテンツを指定します。 任意の数のコンテンツ同期設定を作成できます。 各設定には、識別のための名前が付けられます。

コンテンツ同期設定を作成するには、 `cq:ContentSyncConfig` リポジトリのノードに、 `sling:resourceType` プロパティを `contentsync/config`. この `cq:ContentSyncConfig` ノードはリポジトリ内の任意の場所に配置できますが、AEMパブリッシュインスタンス上のユーザーがそのノードにアクセスできる必要があります。 したがって、以下にノードを追加する必要があります。 `/content`.

コンテンツ同期 ZIP ファイルのコンテンツを指定するには、cq:ContentSyncConfig ノードに子ノードを追加します。 各子ノードの次のプロパティは、含めるコンテンツ項目と、その追加時の処理方法を識別します。

* `path`:コンテンツの場所。
* `type`:コンテンツの処理に使用する設定タイプの名前。 複数のタイプを使用できます。詳しくは、設定タイプを参照してください。

コンテンツ同期設定の例を参照してください。

コンテンツ同期設定を作成すると、その設定がコンテンツ同期コンソールに表示されます。

>[!NOTE]
>
>コンテンツ同期フレームワークは、アセットとデザイン関連のファイルの依存関係がコンテンツ同期パッケージに含まれているかどうかを確認しません。 必要なファイルをすべて ZIP ファイルに含めてください。

### コンテンツ同期ダウンロードへのアクセスの設定 {#configuring-access-to-content-sync-downloads}

コンテンツ同期からダウンロードできるユーザーまたはグループを指定します。 すべてのコンテンツ同期キャッシュからダウンロードできるデフォルトのユーザーまたはグループを設定できます。また、デフォルトを上書きして、特定のコンテンツ同期設定のアクセスを設定できます。

AEMをインストールすると、管理者グループのメンバーは、デフォルトでコンテンツ同期からダウンロードできます。

### コンテンツ同期ダウンロードのデフォルトアクセスの設定 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager サービスは、コンテンツ同期へのアクセスを制御します。 このサービスを設定して、デフォルトでコンテンツ同期からダウンロードできるユーザーまたはグループを指定します。

次の場合、 [Web コンソールを使用したサービスの設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)の場合は、ユーザーまたはグループの名前を Fallback Cache Authorizable プロパティの値として入力します。

次の場合、 [リポジトリでの設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を使用する場合は、このサービスに関する次の情報を使用します。

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* プロパティ名：contentsync.fallback.authorizable

#### コンテンツ同期キャッシュのダウンロードアクセスの上書き {#overriding-download-access-for-a-content-sync-cache}

特定のコンテンツ同期設定のダウンロードアクセスを設定するには、次のプロパティを `cq:ContentSyncConfig` ノード：

* 名前：authorizable
* タイプ：String
* 値：ダウンロード可能なユーザーまたはグループの名前。

例えば、ユーザーがアプリを使用して、コンテンツ同期から直接更新をインストールできるようにします。 すべてのユーザーが更新をダウンロードできるようにするには、authorizable プロパティの値をに設定します。 `everyone`.

この `cq:ContentSyncConfig` ノードに authorizable プロパティがない場合、Day CQ Content Sync Manager サービスの Fallback Cache Authorizable プロパティ用に設定されているデフォルトのユーザーまたはグループが、誰をダウンロードできるかを決定します。

### コンテンツ同期キャッシュを更新するためのユーザーの設定 {#configuring-the-user-for-updating-a-content-sync-cache}

ユーザーがコンテンツ同期キャッシュの更新を実行すると、特定のユーザーアカウントがユーザーに代わってアクションを実行します。 匿名ユーザーは、デフォルトで、すべてのコンテンツ同期キャッシュを更新します。

デフォルトのユーザーを上書きし、特定のコンテンツ同期キャッシュを更新するユーザーまたはグループを指定できます。

デフォルトのユーザーを上書きするには、次のプロパティを cq:ContentSyncConfig ノードに追加して、特定のコンテンツ同期設定の更新を実行するユーザーまたはグループを指定します。

* 名前：updateuser
* タイプ：String
* 値：更新を実行できるユーザーまたはグループの名前。

cq:ContentSyncConfig ノードに updateuser プロパティがない場合、デフォルトの匿名ユーザーがキャッシュを更新します。

### 設定タイプ {#configuration-types}

処理には、単純な JSON のレンダリングから、参照元のアセットを含むページの完全に本格的なレンダリングまで多岐にわたります。 この節では、使用可能な設定タイプとその特定のパラメーターを示します。

**コピー** ファイルとフォルダーをコピーするだけです。

* **パス**  — パスが単一のファイルを指す場合、ファイルのみがコピーされます。 フォルダー（ページノードを含む）を指す場合、以下のすべてのファイルとフォルダーがコピーされます。

**コンテンツ** 標準の Sling リクエスト処理を使用してコンテンツをレンダリングします。

* **パス**  — 出力するリソースのパス。
* **拡張**  — リクエストで使用する拡張子。 一般的な例は次のとおりです。 *html* および *json*&#x200B;ですが、他の拡張は可能です。

* **セレクター**  — オプションのセレクター（ドット区切り）。 一般的な例は次のとおりです。 *タッチ* （ページのモバイルバージョンをレンダリングする場合）または *無限* JSON 出力用。

**clientlib** JavaScript または CSS クライアントライブラリをパッケージ化します。

* **パス**  — クライアントライブラリのルートへのパス。
* **拡張**  — クライアントライブラリのタイプ。 これは、次のいずれかに設定する必要があります。 *js* または *css* 今

* **includeFolders**  — 型は文字列の配列で、クライアントライブラリでスキャンしてファイル（カスタムフォントなど）を取得するための追加のフォルダーをユーザーが指定できます。

**アセット**

アセットのオリジナルのレンディションを収集します。

* **パス** - /content/dam の下のアセットフォルダーのパス。
* **レンディション**  — 型は文字列の配列で、ユーザーはデフォルト画像の代わりに使用するレンディションを指定できます。 次のリストは、既製のレンディションの一部をまとめたものですが、ワークフローで作成された任意のレンディションを使用することもできます。

   * *オリジナル*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**画像** 画像を収集します。

* **パス**  — 画像リソースへのパス。

画像タイプは、We.Retail ロゴを zip ファイルに含めるために使用されます。

**ページ** AEMページをレンダリングし、参照元のアセットを収集します。

* **パス**  — ページへのパス。
* **拡張**  — リクエストで使用する拡張子。 ページの場合、これはほとんど常にです *html*&#x200B;ですが、他の方法もまだ可能です。

* **セレクター**  — オプションのセレクター（ドット区切り）。 一般的な例は次のとおりです。 *タッチ* モバイルバージョンのページをレンダリングする場合。

* **深い**  — 子ページも含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true.*

* **includeImages**  — 画像を含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true*.
デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントのみが含められます。 リソースタイプを追加するには、 **Day CQ WCM Pages Update Handler** Web コンソールの

**書き換え** rewrite ノードは、書き出されたページでリンクを書き換える方法を定義します。 書き換えられたリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指す場合があります。

この `rewrite` ノードは、以下に配置する必要があります。 `page` ノード。

この `rewrite` ノードには、次の 1 つ以上のプロパティを含めることができます。

* `clientlibs`:clientlibs のパスを書き換えます。

* `images`:画像のパスを書き換えます。
* `links`:リンクのパスを書き換えます。

各プロパティは、次のいずれかの値を持つことができます。

* `REWRITE_RELATIVE`:ファイルシステム上の page .html ファイルの相対位置を使用してパスを書き換えます。

* `REWRITE_EXTERNAL`:AEM [Externalizer サービス](/help/sites-developing/externalizer.md).

AEMサービスの名前： **PathRewriterTransformerFactory** では、書き換える特定の html 属性を設定できます。 このサービスは Web コンソールで設定でき、 `rewrite` ノード： `clientlibs`, `images` および `links`.

この機能はAEM 5.5 で追加されました。

### コンテンツ同期設定の例 {#example-content-sync-configuration}

次のリストは、コンテンツ同期の設定例を示しています。

```java
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default と etc.designs.mobile** 設定の最初の 2 つのエントリは、非常に明確である必要があります。 多数のモバイルページを含める場合は、/etc/designs の下に関連するデザインファイルが必要です。 追加の処理は不要なので、コピーで十分です。

**events.plist** このエントリは、少し特別です。 導入で説明したように、アプリケーションは、イベントの位置のマーカーを持つマップビューを提供する必要があります。 必要なロケーション情報は、PLIST 形式の個別のファイルとして提供します。 これを機能させるには、インデックスページで使用されるイベントリストコンポーネントに plist.jsp というスクリプトを使用します。 このスクリプトは、コンポーネントのリソースが.plist 拡張子を持つように要求されたときに実行されます。 通常どおり、コンポーネントのパスは path プロパティで指定され、type は content に設定されます。これは、Sling 要求処理を利用するためです。

**events.touch.html** 次に、アプリに表示される実際のページが表示されます。 path プロパティがイベントのルートページに設定されます。 ディーププロパティのデフォルト値は true なので、そのページ以下のすべてのイベントページも含まれます。 ページを設定タイプとして使用し、画像またはページ上のダウンロードコンポーネントから参照される画像やその他のファイルが含まれるようにします。 また、タッチセレクターを設定すると、モバイルバージョンのページが表示されます。 機能パックの設定には、この種のエントリがさらに含まれていますが、ここでは簡単にするために、これらは省略されています。

**ロゴ** ロゴの設定タイプについては、これまで説明されておらず、組み込みタイプにもなりません。 ただし、コンテンツ同期フレームワークはある程度拡張可能です。これはその一例で、次の節で説明します。

**manifest** 多くの場合、コンテンツの開始ページなど、何らかの種類のメタデータを zip ファイルに含めることが望ましいと考えられます。 ただし、このような情報をハードコーディングすると、後で簡単に変更できなくなります。 コンテンツ同期フレームワークは、設定内のマニフェストノードを探すことでこの使用例をサポートします。このノードは名前で識別されるだけで、設定タイプは不要です。 特定のノードで定義されたすべてのプロパティは、ファイルに追加されます。このファイルは manifest とも呼ばれ、zip ファイルのルートに存在します。

この例では、イベントリストページは最初のページであると想定されています。 この情報は、 **indexPage** これにより、いつでも簡単に変更できるプロパティを作成できます。 2 つ目のプロパティは、 *events.plist* ファイル。 後で説明するように、クライアントアプリケーションはマニフェストを読み取り、それに従って動作できるようになります。

設定が完了し次第、ブラウザーまたはその他の HTTP クライアントを使用してコンテンツをダウンロードできます。iOS用に開発する場合は、専用の WAppKitSync クライアントライブラリを使用できます。 ダウンロード場所は、設定のパスと *.zip* 拡張機能 ( 例：ローカルAEMインスタンスを使用する場合 ): *https://localhost:4502/content/weretail_go.zip*

### コンテンツ同期コンソール {#the-content-sync-console}

コンテンツ同期コンソールには、リポジトリ内のすべてのコンテンツ同期設定（タイプのすべてのノード）がリストされます `cq:ContentSyncConfig`) と各設定で、次の操作を実行できます。

* キャッシュを更新します。
* キャッシュをクリアします。
* 完全な zip をダウンロードします。
* 現在と特定の日時の差分 zip をダウンロードします。

開発やトラブルシューティングに役立ちます。

コンソールには、次の場所からアクセスできます。

`https://localhost:4502/libs/cq/contentsync/content/console.html`

次のようなコンソールが表示されます。

![chlimage_1](assets/chlimage_1.png)

### コンテンツ同期フレームワークの拡張 {#extending-the-content-sync-framework}

設定オプションの数は既にかなり多いものの、特定の使用例のすべての要件を満たしているわけではない場合があります。 この節では、コンテンツ同期フレームワークの拡張ポイントと、カスタム設定タイプの作成方法について説明します。

設定タイプごとに、 *コンテンツ更新ハンドラー*：その特定のタイプに対して登録される OSGi コンポーネントファクトリです。 これらのハンドラーは、コンテンツを収集し、処理し、コンテンツ同期フレームワークで管理されるキャッシュに追加します。 次のインターフェイスまたは抽象基本クラスを実装します。

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — すべての更新ハンドラーが実装する必要があるインターフェイス
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Sling を使用してリソースのレンダリングを簡素化する抽象クラス

クラスを OSGi コンポーネントファクトリとして登録し、バンドルの OSGi コンテナにデプロイします。 これは、 [Maven SCR プラグイン](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) JavaDoc タグまたは注釈の使用 次の例は、JavaDoc のバージョンを示しています。

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

この *工場* 定義には、共通インターフェイスとカスタムタイプをスラッシュで区切って含めます。 この方法では、コンテンツ同期フレームワークが設定エントリでカスタムタイプを認識し、カスタムクラスのインスタンスを検索して作成できます。 次の節では、カスタム更新ハンドラの具体的な例を示します。

>[!CAUTION]
>
>AbstractSlingResourceUpdateHandler 基本クラスに基づいて構築する場合、 *継承* 定義。 そうしないと、OSGi コンテナは、基本クラスで宣言されている必要な参照を設定しません。

### カスタム更新ハンドラーの実装 {#implementing-a-custom-update-handler}

すべての We.Retail Mobile ページの左上隅には、もちろん zip ファイルに含めたいロゴが含まれています。 ただし、キャッシュの最適化の場合、AEMは画像ファイルのリポジトリ内の実際の場所を参照しないので、 **コピー** 設定タイプ。 代わりに、独自の **ロゴ** AEMが要求した場所で画像を使用できるようにする設定タイプ。 次のコードリストは、ロゴ更新ハンドラーの完全な実装を示しています。

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

この `LogoUpdateHandler` クラスは、 `ContentUpdateHandler` インターフェイスの `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` メソッドを使用します。このメソッドは、次のように多数の引数を取ります。

* A `ConfigEntry` このハンドラーが呼び出される設定エントリとそのプロパティへのアクセスを提供するインスタンス。
* A `lastUpdated` コンテンツ同期が最後にキャッシュを更新した時刻を示すタイムスタンプ。 その後に変更されていないコンテンツは、ハンドラーによって更新されないでください。
* A `configCacheRoot` キャッシュのルートパスを指定する引数。 更新されたすべてのファイルを zip ファイルに追加するには、このパスの下に保存する必要があります。
* すべてのキャッシュ関連リポジトリ操作に使用する必要がある管理セッション。
* 特定のユーザーのコンテキストでコンテンツを更新し、パーソナライズされたコンテンツの一種を提供するために使用できるユーザーセッション。

カスタムハンドラーを実装するには、まず、設定エントリで指定されたリソースに基づいて Image クラスのインスタンスを作成します。 これは、基本的に、ページ上の実際のロゴコンポーネントと同じ手順です。 画像のターゲットパスは、ページから参照されたパスと同じにする必要があります。

次に、前回の更新以降にリソースが変更されたかどうかを確認します。 カスタム実装では、キャッシュの不要な更新を避け、何も変更しない場合は false を返す必要があります。 リソースが変更された場合は、キャッシュのルートを基準とした適切なターゲット位置に画像をコピーします。 最後に `true` がフレームワークに返され、キャッシュが更新されたことが示されます。

## クライアントでのコンテンツの使用 {#using-the-content-on-the-client}

コンテンツ同期で提供されるモバイルアプリでコンテンツを使用するには、HTTP または HTTPS 接続を介してコンテンツをリクエストする必要があります。 その結果、取得したコンテンツ（ZIP ファイルにパック）を抽出し、モバイルデバイス上でローカルに保存することができます。 コンテンツとは、データだけでなくロジック（完全な Web アプリケーション）も指すことに注意してください。これにより、ネットワークに接続していなくても、モバイルユーザは検索したウェブアプリケーション及び対応するデータを実行することができる。

コンテンツ同期は、インテリジェントな方法でコンテンツを提供します。最後に正常にデータ同期が配信されてからのデータ変更のみがおこなわれるので、データ転送に必要な時間が短縮されます。 1970 年 1 月 1 日以降、アプリケーションデータの初回実行時に変更がリクエストされ、その後、前回正常に同期された後に変更されたデータのみがリクエストされます。 AEMは、iOSのクライアント通信フレームワークを利用して、データ通信と転送を簡素化し、iOSベースの Web アプリケーションを有効にするために最小限のネイティブコードが必要になるようにします。

転送されたすべてのデータは同じディレクトリ構造に抽出でき、データを抽出する際に追加の手順（依存関係チェックなど）は必要ありません。 iOSの場合、すべてのデータはiOSアプリの Documents フォルダー内のサブフォルダーに保存されます。

iOSベースのAEM Mobileアプリの一般的な実行パス：

* ユーザーがiOSデバイスでアプリを起動します。
* アプリはAEMバックエンドに接続しようとし、前回の実行以降にデータの変更をリクエストします。
* サーバーは問題のデータを取得し、ファイルに zip ファイルに送信します。
* データはクライアントデバイスに返され、ドキュメントフォルダーに抽出されます。
* UIWebView コンポーネントは、開始/更新します。

接続を確立できなかった場合は、以前にダウンロードしたデータが表示されます。

### 先に進む {#getting-ahead}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
