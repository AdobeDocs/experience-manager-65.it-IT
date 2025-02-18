---
title: Eventi OSGi per componenti community
description: Vengono inviati eventi OSGi che possono attivare i listener asincroni
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
source-wordcount: '592'
ht-degree: 5%

---

# Eventi OSGi per componenti community  {#osgi-events-for-communities-components}

## Panoramica {#overview}

Quando i membri interagiscono con le funzioni di Communities, vengono inviati eventi OSGi che possono attivare listener asincroni, come notifiche o gamification (punteggio e badge).

L&#39;istanza [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) di un componente registra gli eventi come `actions` che si verificano per un `topic`. SocialEvent include un metodo per restituire un `verb` associato all&#39;azione. Esiste una relazione *n-1* tra `actions` e `verbs`.

Per i componenti Community consegnati nella versione, le tabelle seguenti descrivono i `verbs` definiti per ogni `topic` disponibile.

## Argomenti e verbi {#topics-and-verbs}

[Componente Calendario](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un evento calendario |
| AGGIUNGI | Commenti dei membri su un evento calendario |
| AGGIORNA | Il commento o l&#39;evento calendario del membro è stato modificato |
| ELIMINA | Il commento o l&#39;evento calendario del membro viene eliminato |

[Componente Commenti](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un commento |
| AGGIUNGI | Risposte dei membri al commento |
| AGGIORNA | Commento del membro modificato |
| ELIMINA | Commento del membro eliminato |

[Componente Libreria File](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea una cartella |
| ALLEGA | Il membro carica un file |
| AGGIORNA | Il membro aggiorna una cartella o un file |
| ELIMINA | Il membro elimina una cartella o un file |

[Componente forum](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea l&#39;argomento forum |
| AGGIUNGI | Risposte dei membri all&#39;argomento forum |
| AGGIORNA | L&#39;argomento del forum o la risposta del membro è stato modificato |
| ELIMINA | L&#39;argomento del forum o la risposta del membro è stata eliminata |

[Componente diario](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un articolo di blog |
| AGGIUNGI | Commenti dei membri su un articolo del blog |
| AGGIORNA | L&#39;articolo o il commento del blog del membro è stato modificato |
| ELIMINA | L&#39;articolo o il commento del blog del membro è stato eliminato |

[Componente QnA](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea una domanda di controllo qualità |
| AGGIUNGI | Il membro crea una risposta QnA |
| AGGIORNA | Domanda o risposta QnA del membro modificata |
| SELEZIONA | Risposta del membro selezionata |
| DESELEZIONA | La risposta del membro è deselezionata |
| ELIMINA | La domanda o la risposta QnA del membro viene eliminata |

[Componente recensioni](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea la revisione |
| AGGIORNA | Revisione del membro modificata |
| ELIMINA | Revisione del membro eliminata |

[Componente valutazione](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VALUTAZIONE | Il contenuto dell&#39;utente è stato rivalutato |
| RIMUOVI VALUTAZIONE | Il contenuto dell&#39;utente non è stato valutato correttamente |

[Componente Votazione](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VOTAZIONE | Il contenuto del membro è stato votato |
| RIMUOVI VOTAZIONE | Il contenuto del membro non è stato votato |

**Componenti abilitati per moderazione**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrizione** |
|---|---|
| RIFIUTA | Contenuto dell&#39;utente negato |
| SEGNALA COME INAPPROPRIATO | Il contenuto del membro è contrassegnato |
| ANNULLA SEGNALAZIONE COME INAPPROPRIATO | Il contenuto del membro non è contrassegnato |
| ACCETTA | Il contenuto del membro è approvato dal moderatore |
| CHIUDI | Il membro chiude il commento alle modifiche e alle risposte |
| APRI | Il membro riapre il commento |

## Eventi per componenti personalizzati {#events-for-custom-components}

Per un componente personalizzato, la [classe astratta SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) deve essere estesa d per registrare gli eventi del componente come `actions` che si verificano per un `topic`.

L&#39;evento personalizzato eseguirà l&#39;override del metodo `getVerb()` in modo che venga restituito un `verb` appropriato per ogni `action`. Il `verb` restituito per un&#39;azione può essere uno usato comunemente (ad esempio `POST`) o uno specializzato per il componente (ad esempio `ADD RATING`). Esiste una relazione *n-1* tra `actions` e `verbs`.

>[!NOTE]
>
>Assicurati che un’estensione personalizzata sia registrata con una classificazione inferiore rispetto a qualsiasi implementazione esistente nel prodotto.

### Pseudo-codice per evento componente personalizzato {#pseudo-code-for-custom-component-event}

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

## Esempio di EventListener per filtrare i dati del flusso di attività {#sample-eventlistener-to-filter-activity-stream-data}

È possibile ascoltare gli eventi allo scopo di modificare ciò che appare nel flusso di attività.

Il seguente pseudo-codice di esempio rimuoverà gli eventi DELETE per il componente Comments dal flusso di attività.

### Pseudo-codice per EventListener {#pseudo-code-for-eventlistener}

Richiede [pacchetto di funzionalità più recente](deploy-communities.md#latestfeaturepack).

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
