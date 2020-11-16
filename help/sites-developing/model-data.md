---
title: データのモデル化 - David Nuescheler のモデル
seo-title: データのモデル化 - David Nuescheler のモデル
description: David Nuescheler のコンテンツモデル化の推奨事項
seo-description: David Nuescheler のコンテンツモデル化の推奨事項
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 80%

---


# データのモデル化 - David Nuescheler のモデル{#data-modeling-david-nuescheler-s-model}

## ソース {#source}

以下の詳細は、David Nuescheler 氏が表明している見解です。

同氏は、アドビが 2010 年に買収した、グローバルなコンテンツ管理およびコンテンツインフラストラクチャソフトウェアの大手プロバイダーである Day Software AG 社の共同創立者兼 CTO です。現在は、アドビのフェローであり、Enterprise Technology のバイスプレジデントです。また、コンテンツ管理の技術標準である Java コンテンツリポジトリ（JCR）アプリケーションプログラミングインターフェイス（API）、JSR-170 開発の第一人者でもあります。

Further updates can also be seen on [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## David からのあいさつ {#introduction-from-david}

様々な話し合いの中で、コンテンツのモデル化という点では、JCR の機能に関して開発者たちが幾分不安を感じていることがわかりました。リポジトリ内のコンテンツをモデル化する方法や、コンテンツモデルの中に優劣が存在する理由については、まだ何の指針もなく、経験もほとんどありません。

リレーショナルな世界では、ソフトウェア業界にはデータのモデル化に関して多くの経験がありますが、コンテンツリポジトリに関しては、まだ初期段階です。

コンテンツをモデル化する方法について私の個人的意見を表明することにより、この空白を埋める試みを始めたいと思います。これがいずれ開発者コミュニティにとってより有意義なものへと変化し、単なる「私の意見」ではなく、より一般的なものとなることを期待しています。よって、これは私の最初の挑戦であり、今後急速に進化するものとお考えください。

>[!NOTE]
>
>免責事項：このガイドラインは、私個人の見解であり、賛否が分かれる場合もあります。内容について意見を交わし、改善することを期待しています。

## 簡単な 7 つのルール {#seven-simple-rules}

### Rule #1: Data first, structure later. Maybe. {#rule-data-first-structure-later-maybe}

#### 説明 {#explanation-1}

ERD の意味では、宣言されているデータ構造について気にしないことをお勧めします。ただし、最初のうちは、です。

開発の際は、nt:unstructured（およびその仲間たち）を好きになるようにしてください。

これについては Stefano さんがよくまとめてくれると思います。

私の結論としては、構造はコストがかかるものであり、多くの場合、基になるストレージに対して構造を明示的に宣言することはまったく必要ありません。

アプリケーションで使用することになっている構造に関しては、暗黙の契約があります。例えば、ブログの投稿の変更日を lastModified プロパティに格納するとします。アプリケーションでは、その同じプロパティから再度変更日を読み取ることが自動的に認識されるので、明示的に宣言する必要はまったくありません。

必須などの追加のデータ制約や、タイプや値の制約は、データの整合性のために必要な場合にのみ適用します。

#### 例 {#example-1}

上記の例で、「ブログ投稿」ノードなどで `lastModified` 日付プロパティを使用する場合は、特別なノードタイプが必要であるとは限りません。 最初は、ブログ投稿ノード `nt:unstructured` に必ず使用します。 ブログアプリでは、lastModified日付を表示するだけなので（「順番」を付けても）、日付になってもほとんど気にしません。 私はブログ書きの申込書を暗黙的に信頼して&quot;date&quot;をそこに置くので、nodetypeの形式の `lastModified` 日付の存在を宣言する必要はありません。

### Rule #2: Drive the content hierarchy, don&#39;t let it happen. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 説明 {#explanation-2}

コンテンツ階層は非常に価値の高いアセットです。だから、それを実現させるのはやめ、設計してみてください。 ノードに「良い」人間が読み取り可能な名前がない場合は、それを再考する必要があると思います。 任意の数字が「良い名前」とはほとんど言えません。

既存のリレーショナルモデルをすぐに階層モデルに変換できれば非常に簡単かもしれませんが、その際は多少の配慮が必要です。

私の経験では、アクセス制御および抑制によってコンテンツ階層を駆動させるという考えが多いようです。コンテンツ階層を、自分のファイルシステムと考えてください。ファイルやフォルダーを使用して、ローカルディスク上でモデル化することも可能です。

個人的には、多くの場合、最初はノードタイピングシステム経由で階層を変換し、後からタイピングを導入する方法を好みます。

>[!CAUTION]
>
>コンテンツリポジトリの構造化の方法はパフォーマンスにも影響を及ぼす可能性があります。最適なパフォーマンスを確保するために、コンテンツリポジトリ内の個々のノードに接続される子ノードの数は、通常 1,000 個以下にする必要があります。
>
>CRXで処理でき [るデータ量を参照してください。](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) を参照してください。

#### 例 {#example-2}

以下のような単純なブログシステムをモデル化します。この時点で使用する個々のノードタイプについて、最初は気にしてさえいないことに注目してください。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

私が明らかになったのは、この例に基づく内容の構造を理解している人が、それ以上の説明をすることなくいることです。

「コメント（comments）」を「投稿（post）」と共に格納しないことを最初は疑問にお思いかもしれませんが、これは、アクセス制御を合理的に階層化された方法で適用したいからです。

上記のコンテンツモデルを使用すると、「匿名の」ユーザーにコメントの「作成」を簡単に許可する一方で、匿名のユーザーを残りのワークスペースで読み取り専用ベースに保つことができます。

### ルール 3：ワークスペースは clone()、merge() および update() 用。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 説明 {#explanation-3}

If you don&#39;t use `clone()`, `merge()` or `update()` methods in your application a single workspace is probably the way to go.

「対応するノード」は、JCR 仕様で定義されている概念です。結局のところは、本質的に、それぞれ異なるいわゆるワークスペース内の、同じコンテンツを表すノードのことです。

JCR ではワークスペースの概念が非常に抽象的に紹介されているので、何に使用すればよいのか、開発者には不明瞭なままになっています。ワークスペースを、以下のようにテスト目的で使用することを提案します。

「対応する」ノード（基本的には同じ UUID を持つノード）が、複数のワークスペースに多数重複している場合は、ワークスペースをうまく使用している可能性が高いでしょう。

同じ UUID を持つノードの重複がまったくない場合は、ワークスペースの使い方が誤っている可能性があります。

ワークスペースは、アクセス制御には使用しないでください。特定のユーザーグループにコンテンツを表示することは、別々のワークスペースに分割する十分な根拠とはなりません。JCR には、このためにコンテンツリポジトリの「アクセス制御」機能が用意されています。

ワークスペースは、参照およびクエリの境界です。

#### 例 {#example-3}

ワークスペースは、次のようなものに使用します。

* プロジェクトの v1.2 とプロジェクトの v1.3
* コンテンツの「開発」、「QA」および「公開済み」の状態

ワークスペースは、次のようなものには使用しないでください。

* ユーザーのホームディレクトリ
* 公開、非公開、ローカルなど、様々なターゲットオーディエンスの明確なコンテンツ
* 様々なユーザーのメールインボックス

### ルール 4：同じ名前の兄弟に注意。 {#rule-beware-of-same-name-siblings}

#### 説明 {#explanation-4}

同じ名前の兄弟（SNS）は、XML 用に設計され、XML で表現されているデータ構造との互換性を得るために仕様に導入されたので、JCR にとって非常に有益ではありますが、リポジトリのオーバーヘッドが大きく、かなり複雑です。

いずれかのパスセグメントに SNS が含まれているコンテンツリポジトリのパスは安定性が非常に低くなり、1 つの SNS が削除されるか並べ替えられると、その他すべての SNS およびそれぞれの子のパスに影響します。

XML の読み込みや既存の XML とのインタラクションのために SNS が必要かつ便利な場合もありますが、私は SNS を使用したことはなく、ゼロから始めるデータモデルでは今後も使用することはありません。

#### 例 {#example-4}

使用方法

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

以下の代わりに使用します。

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### ルール 5：参照は有害と見なされる。 {#rule-references-considered-harmful}

#### 説明 {#explanation-5}

参照は参照整合性を暗示します。参照を使用すると、参照整合性を管理するリポジトリのコストが増加するだけでなく、コンテンツの柔軟性という点からもコストがかかることを理解することが重要です。

個人的には、定まっていない参照をどうしても処理できない場合にのみ参照を使用し、それ以外の場合はパス、名前、文字列 UUID のいずれかを使用して別のノードを参照するようにしています。

#### 例 {#example-5}

ドキュメント（a）からドキュメント（b）への「参照」を許可すると仮定しましょう。参照プロパティを使用してこの関係をモデル化する場合、2 つのドキュメントはリポジトリレベルでリンクされるということです。参照プロパティのターゲットが存在しない可能性があるので、ドキュメント（a）の個別の書き出しや読み込みはできません。統合、更新、復元、クローンなど、その他の操作も同様に影響を受けます。

したがって、私はこれらの参照を「弱い参照」（JCR v1.0 では、結局のところターゲットノードの UUID を含む文字列プロパティ）としてモデル化するか、単純にパスを使用します。そもそも、パスのほうが有意である場合もあります。

参照が定まっていないとシステムが機能しない場合があると思いますが、私の実体験からは、十分に「現実的」で、かつシンプルな例は、思いつきません。

### Rule #6: Files are files. {#rule-files-are-files}

#### 説明 {#explanation-6}

If a content model exposes something that even remotely *smells* like a file or a folder I try to use (or extend from) `nt:file`, `nt:folder` and `nt:resource`.

私の経験では、多くの汎用アプリケーションで、nt:folder および nt:files とのインタラクションが暗黙的に許可されており、メタ情報が追加された場合にイベントを処理して表示する方法が認識されています。例えば、JCR をベースとしている CIFS や WebDAV のようなファイルサーバー実装との直接のインタラクションは暗黙となります。

大ざっぱに言えば、次のようなものが使えると思う。ファイル名とMIME型を格納する必要がある場合、/は `nt:file`非常に適 `nt:resource` しています。 複数の「ファイル」を保存できる場合は、nt:folderを保存するのが適切です。

リソースにメタ情報を追加する必要がある場合は、「author」プロパティや「description」プロパティなど、「author」プロパティや「description」プロパティを追加する必要はありま `nt:resource` せん `nt:file`。 nt:fileを拡張することはほとんどありませんが、頻繁に拡張し `nt:resource`ます。

#### 例 {#example-6}

誰かが以下のブログに画像をアップロードしたいと仮定します。

```xml
/content/myblog/posts/iphone_shipping
```

最初の直感的反応は、画像を含むバイナリプロパティを追加することになるでしょう。

バイナリプロパティだけを使用する良い使用例ももちろんありますが（名前は重要でなく、MIME タイプは暗黙であるとします）、この場合、私のブログ例には、以下の構造をお勧めします。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### ルール 7：ID は悪である。 {#rule-ids-are-evil}

#### 説明 {#explanation-7}

リレーショナルデータベースでは、ID は関係を表すのに必要な手段なので、コンテンツモデルでも ID が使用される傾向があります。ただし、多くは誤った理由によるものです。

コンテンツモデルがプロパティでいっぱいで、「ID」で終わっている場合は、階層が適切に活用されていない可能性があります。

確かに、一部のノードでは、ライフサイクル全体に渡って安定した識別が必要です。ただし、そのようなノードはそれほど多くありません。mix:referenceable によって、このようなメカニズムがリポジトリに組み込まれるので、安定した方法でノードを識別する方法を追加で考え出す必要はありません。

項目はパスによっても識別できることも心に留めておいてください。UNIX ファイルシステムで「シンボリックリンク」が多くのユーザーにとってハードリンクよりはるかに大きな意味を持つのと同様に、ターゲットノードを参照する場合は、ほとんどのアプリケーションでパスが意味を持ちます。

More importantly, it is **mix**:referenceable which means that it can be applied to a node at the point in time when you actually need to reference it.

よって、タイプが「ドキュメント」であるノードを参照可能にしたいからといって、「ドキュメント」ノードタイプを静的な方法で mix:referenceable から拡張しなければならないということにはなりません。「ドキュメント」の任意のインスタンスに動的に追加できるからです。

#### 例 {#example-7}

使用方法:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

以下の代わりに使用します。

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```

