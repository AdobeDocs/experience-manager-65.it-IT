---
title: Notifiche community
seo-title: Notifiche community
description: ' AEM Communities dispone di notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l''accesso'
seo-description: ' AEM Communities dispone di notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l''accesso'
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# Notifiche community {#communities-notifications}

## Panoramica {#overview}

 AEM Communities fornisce una sezione delle notifiche che mostra gli eventi di interesse per i membri della community sottoscritti.

Le notifiche sono simili alle [attività](/help/communities/essentials-activities.md) e alle [iscrizioni](/help/communities/subscriptions.md), in quanto possono derivare da:

* Il contenuto di pubblicazione del membro.
* Il membro che sceglie di seguire un altro membro.
* Il membro che sceglie di seguire argomenti, articoli e altri thread specifici di contenuto.
* Il membro con tag (@reference) un altro membro della community in un contenuto generato dall&#39;utente.

Ciò che distingue le notifiche dalle attività e dalle sottoscrizioni è:

* Un collegamento alla sezione delle notifiche è sempre presente nell&#39;intestazione di un sito community:

   * Le attività richiedono che la [funzione del flusso di attività](/help/communities/functions.md#activity-stream-function) sia inclusa nella struttura del sito community.
   * Le iscrizioni richiedono [la configurazione di email](/help/communities/email.md).

* L&#39;implementazione delle notifiche avviene tramite canali scalabili e collegabili:

   * Le attività sono disponibili solo sul Web.
   * Le iscrizioni sono disponibili solo tramite e-mail.

Per quanto riguarda le community [FP1](/help/communities/deploy-communities.md#latestfeaturepack), i canali di notifica disponibili sono:

* Canale Web a cui si accede utilizzando il collegamento `Notifications`.
* Il canale e-mail, disponibile quando l’e-mail è configurata correttamente.

I canali futuri sono mobile e desktop.

### Requisiti {#requirements}

**Configura e-mail**

Affinché il canale e-mail possa funzionare, è necessario configurare l’e-mail.

Per istruzioni sulla configurazione dell&#39;e-mail, vedere [Configurazione di e-mail](/help/communities/analytics.md).

**Abilita Follow**

I componenti devono essere configurati per abilitare quanto segue. Le funzioni che consentono di seguire sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) e [commenti](/help/communities/comments.md).

**Nota**:

* I componenti utilizzati all&#39;interno di [modelli di sito](/help/communities/sites.md) e [modelli di gruppo](/help/communities/tools-groups.md) community possono già essere configurati per seguirli.

* I profili dei membri sono già configurati per consentire agli altri membri di seguirli.

## Notifiche da {#notifications-from-following}

![notifiche](assets/notifications.png)

Il pulsante **[!UICONTROL Segui]** consente di seguire le voci come attività, iscrizioni e/o notifiche. Ogni volta che il tasto **[!UICONTROL Segui]** è selezionato, è possibile attivare o disattivare una selezione. La selezione `Email Subscriptions` è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **[!UICONTROL Successivo]**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **[!UICONTROL Segui]**:

* Quando si visualizza il profilo di un altro membro.
* In una pagina delle funzioni principali, ad esempio forum, QnA e blog:

   * Segue tutta l&#39;attività per quella funzione generale.

* Per un post specifico, ad esempio un argomento del forum, una domanda QnA o un articolo di blog:

   * Segue tutta l&#39;attività per quella voce specifica.

## Gestione delle impostazioni di notifica {#managing-notification-settings}

Selezionando il collegamento Impostazioni notifica dalla pagina Notifiche, è possibile per ciascun membro gestire il modo in cui vengono ricevute le notifiche.

Il canale Web è sempre abilitato.

![notifications14](assets/notifications1.png)

Il canale e-mail, che si basa sulla corretta [configurazione di email](/help/communities/email.md), fornisce le stesse impostazioni del canale Web.

Il canale e-mail è disattivato per impostazione predefinita.

![notifiche2](assets/notifications2.png)

Può essere attivata da un membro, ma dipende comunque dalla configurazione dell&#39;e-mail.

![notifiche3](assets/notifications3.png)

## Visualizzazione delle notifiche {#viewing-notifications}

### Notifiche Web {#web-notifications}

Una [procedura guidata creata per la community site](/help/communities/sites-console.md) ora include un collegamento alla funzionalità `Notifications` nella barra dell&#39;intestazione del sito sopra il banner. A differenza dei messaggi, le notifiche vengono create per ogni sito community, mentre i messaggi devono essere attivati durante il processo di creazione del sito.

Quando si visita il sito pubblicato, selezionando il collegamento `Notifications` vengono visualizzate tutte le notifiche relative al membro.

![notifiche4](assets/notifications4.png)

### Notifiche e-mail {#email-notifications}

Quando il canale e-mail è abilitato, il membro riceve un messaggio e-mail contenente un collegamento al contenuto sul Web.

![notifications5](assets/notifications5.png)

## Personalizzare le notifiche e-mail {#customize-email-notifications}

Le organizzazioni possono personalizzare le notifiche e-mail sovrapponendo [i modelli in **/libs/settings/community/templates/email/html**.](/help/communities/client-customize.md#overlays)

Ad esempio, per modificare le notifiche e-mail di menzioni (per un componente community), aggiungere una condizione **if** per il verbo **menzionare** nei modelli dei componenti per i quali è stato abilitato il supporto **@menzioni**.

Per modificare il modello di notifiche e-mail per @Menzioni nei commenti del blog, posizionate fuori dalla casella in: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

