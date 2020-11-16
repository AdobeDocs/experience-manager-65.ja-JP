---
title: OSGi バンドル
seo-title: OSGi バンドル
description: OSGi バンドルを管理するためのヒント
seo-description: OSGi バンドルを管理するためのヒント
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 64%

---


# OSGi バンドル{#osgi-bundles}

## セマンティックバージョニングを使用する {#use-semantic-versioning}

Agreed upon best practices for semantic version numbering can be found at [https://semver.org/](https://semver.org/).

## 厳密に必要な数を超えるクラスおよび jar を OSGi バンドルに埋め込まない {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

共通ライブラリは個別のバンドルに取り出す必要があります。これで、共通ライブラリをバンドル全体で再利用できるようになります。OSGi バンドルに *JAR* をラップするときは、オンラインソースを調べて、誰かが既にこのラップをおこなっていないかどうかを確認してください。既存のバンドルラッパーを探す一般的な場所としては、Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes および SpringSource Enterprise Bundle Repository があります。

## 最低限必要なバンドルバージョンに依存する {#depend-on-the-lowest-needed-bundle-versions}

POM ファイルのコンパイル時依存関係の場合、常に、必要な API を公開するために最低限必要なバージョンに依存するようにします。これにより、後方互換性が高くなり、古いリリースのバックポートの修正が容易になります。

## OSGi バンドルから最小限のパッケージセットをエクスポートする {#export-a-minimal-set-of-packages-from-osgi-bundles}

パッケージのエクスポートが完了したら、すぐに他のユーザーが依存する API を作成しておきます。書き出しはできるだけ少なくし、書き出されるものがAPIであることを確認します。 以前に書き出されたものを取り出してプライベートにするよりも、プライベートメソッド/クラスを取って公開する方がずっと簡単です。

実装は、必ず個別の *impl* パッケージに配置する必要があります。デフォルトでは、*maven-bundle-plugin* は、名前に *impl* が含まれていないプロジェクトにあるものをすべてエクスポートします。

## エクスポートしたパッケージごとに必ずセマンティックバージョニングを明示的に定義する {#always-explicitly-define-a-semantic-version-for-each-package-exported}

このようにすることで、API の利用者も新しいバージョンに取り組むことができます。その場合は、必ずセマンティックのバージョン管理のベストプラクティスに従ってください。 これにより、APIの利用者は、新しいバージョンで予想される変更のタイプを知ることができます。

## 公開場所に関するメタタイプ情報を含める {#include-metatype-information-where-exposed}

意味のあるメタタイプ情報を指定することで、Felix コンソールでのサービスおよびコンポーネントが理解しやすくなります。A list of SCR annotations and attributes can be found at: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
