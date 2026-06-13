---
title: コミュニティコンポーネントの OSGi イベント
description: 非同期リスナーをトリガーできるOSGi イベントが送信される
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 6%

---

# コミュニティコンポーネントの OSGi イベント  {#osgi-events-for-communities-components}

## 概要 {#overview}

メンバーがCommunities機能を操作すると、通知やgamification（スコアリングやバッジ）などの非同期リスナーをトリガーできるOSGi イベントが送信されます。

コンポーネントの[SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) インスタンスは、イベントを`topic`に対して発生した`actions`として記録します。 SocialEventには、アクションに関連付けられた`verb`を返すメソッドが含まれています。 `actions`と`verbs`の間に&#x200B;*n-1*&#x200B;関係があります。

リリースで配信されたCommunities コンポーネントについて、次の表は、使用可能な各`topic`に対して定義された`verbs`を示しています。

## トピックと動詞 {#topics-and-verbs}

[ カレンダーコンポーネント](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **動詞** | **説明** |
|---|---|
| POST | メンバーがカレンダーイベントを作成 |
| 追加 | カレンダーイベントに対するメンバーコメント |
| 更新 | メンバーのカレンダーイベントまたはコメントが編集されます |
| 削除 | メンバーのカレンダーイベントまたはコメントが削除されます |

[ コメントコンポーネント](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **動詞** | **説明** |
|---|---|
| POST | メンバーがコメントを作成します |
| 追加 | メンバーがコメントに返信 |
| 更新 | メンバーのコメントが編集されました |
| 削除 | メンバーのコメントが削除されました |

[ ファイルライブラリコンポーネント](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォルダーを作成します |
| 添付 | メンバーがファイルをアップロード |
| 更新 | メンバーはフォルダーまたはファイルを更新します |
| 削除 | メンバーはフォルダーまたはファイルを削除します |

[ フォーラムコンポーネント](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォーラムのトピックを作成 |
| 追加 | フォーラムのトピックに対するメンバーの返信 |
| 更新 | メンバーのフォーラムのトピックまたは返信が編集されています |
| 削除 | メンバーのフォーラム トピックまたは返信が削除されました |

[ ジャーナルコンポーネント](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **動詞** | **説明** |
|---|---|
| POST | メンバーがブログ記事を作成する |
| 追加 | ブログ記事へのメンバーコメント |
| 更新 | メンバーのブログ記事またはコメントが編集されました |
| 削除 | メンバーのブログ記事またはコメントが削除されました |

[QnA コンポーネント](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **動詞** | **説明** |
|---|---|
| POST | メンバーはQnA質問を作成します |
| 追加 | メンバーがQnA回答を作成 |
| 更新 | メンバーのQnAの質問または回答が編集されます |
| SELECT | メンバーの回答が選択されています |
| 選択解除 | メンバーの回答が選択解除されました |
| 削除 | メンバーのQnAの質問または回答が削除されます |

[ レビューコンポーネント](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **動詞** | **説明** |
|---|---|
| POST | メンバーによるレビューの作成 |
| 更新 | メンバーのレビューが編集されました |
| 削除 | メンバーのレビューが削除されました |

[評価コンポーネント](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **動詞** | **説明** |
|---|---|
| 評価を追加 | メンバーのコンテンツが評価されました |
| 評価を削除 | メンバーのコンテンツがダウン評価されています |

[投票コンポーネント](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **動詞** | **説明** |
|---|---|
| 投票を追加 | メンバーのコンテンツが投票されました |
| 投票を削除 | メンバーのコンテンツがダウンしています |

**モデレーション対応コンポーネント**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **動詞** | **説明** |
|---|---|
| 拒否 | メンバーのコンテンツが拒否されました |
| 不適切なフラグ | メンバーのコンテンツにフラグが付けられている |
| 不適切なフラグを付けない | メンバーのコンテンツにフラグが付いていません |
| 承認 | メンバーのコンテンツはモデレーターによって承認されます |
| 閉じる | メンバーが編集と返信にコメントを閉じる |
| オープン | メンバーがコメントを再度開きます |

## カスタムコンポーネントのイベント {#events-for-custom-components}

カスタムコンポーネントの場合、`topic`に対して発生するコンポーネントのイベントを`actions`として記録するには、[SocialEvent抽象クラス ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)を拡張する必要があります。

カスタムイベントはメソッド `getVerb()`を上書きして、各`action`に適切な`verb`を返します。 アクションに対して返される`verb`は、一般的に使用される1つ（例：`POST`）またはコンポーネントに特化した1つ（例：`ADD RATING`）です。 `actions`と`verbs`の間に&#x200B;*n-1*&#x200B;関係があります。

>[!NOTE]
>
>カスタム拡張機能が、製品内の既存の実装よりも低いランキングで登録されていることを確認します。

### カスタムコンポーネントイベントの疑似コード {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## Activity Stream データをフィルタリングするEventListenerのサンプル {#sample-eventlistener-to-filter-activity-stream-data}

アクティビティストリームに表示される内容を変更する目的で、イベントをリッスンできます。

次の疑似コードサンプルは、DELETEのComments用イベントをアクティビティストリームから削除します。

### EventListenerの疑似コード {#pseudo-code-for-eventlistener}

[最新の機能パック ](deploy-communities.md#latestfeaturepack)が必要です。

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```
