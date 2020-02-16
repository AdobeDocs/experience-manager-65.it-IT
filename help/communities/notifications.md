---
title: Notifiche community
seo-title: Notifiche community
description: AEM Communities dispone di notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l'accesso
seo-description: AEM Communities dispone di notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l'accesso
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Notifiche community{#communities-notifications}

## Panoramica {#overview}

In AEM Communities è disponibile una sezione che mostra gli eventi di interesse per i membri della community sottoscritti.

Le notifiche sono simili alle [attività](/help/communities/essentials-activities.md) e alle [sottoscrizioni](/help/communities/subscriptions.md) derivanti da

* il contenuto di pubblicazione del membro
* il membro che sceglie di seguire un altro membro
* il membro che sceglie di seguire argomenti, articoli e altri thread specifici di contenuto
* il tag del membro (@reference) un altro membro della community in un contenuto generato dall&#39;utente

Ciò che distingue le notifiche dalle attività e dalle sottoscrizioni è

* un collegamento alla sezione delle notifiche è sempre presente nell&#39;intestazione di un sito community

   * le attività richiedono che la funzione [del flusso di](/help/communities/functions.md#activity-stream-function) attività sia inclusa nella struttura del sito comunitario
   * le sottoscrizioni richiedono [la configurazione dell&#39;e-mail](/help/communities/email.md)

* l&#39;implementazione delle notifiche avviene tramite canali scalabili e collegabili

   * le attività sono disponibili solo sul Web
   * le iscrizioni sono disponibili solo tramite e-mail

A livello di Community [FP1](/help/communities/deploy-communities.md#latestfeaturepack), i canali di notifica disponibili sono

* il canale Web a cui si accede tramite il `Notifications` collegamento
* il canale e-mail, disponibile quando l&#39;e-mail è configurato correttamente

I canali futuri sono mobile e desktop.

### Requisiti {#requirements}

**Configura e-mail**

Affinché il canale e-mail possa funzionare, è necessario configurare l’e-mail.

Per istruzioni sulla configurazione dell’e-mail, consultate [Configurazione dell’e-mail](/help/communities/analytics.md).

**Abilita Follow**

I componenti devono essere configurati per abilitare quanto segue. Le funzioni che consentono di seguire sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filibreria](/help/communities/file-library.md)[](/help/communities/comments.md), commenti.

Tieni presente che

* i componenti utilizzati all&#39;interno di modelli [di](/help/communities/sites.md) sito community e modelli [di](/help/communities/tools-groups.md) gruppo possono già essere configurati per consentire:

* i profili membri sono già configurati per consentire agli altri membri di seguire

## Notifiche dai seguenti {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

Il tasto **Follow **fornisce un mezzo per seguire le voci come attività, iscrizioni e/o notifiche. Ogni volta che il tasto **Follow **è selezionato, è possibile attivare o disattivare una selezione. La `Email Subscriptions` selezione è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **Seguente**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **Follow **I

* quando si visualizza il profilo di un altro membro
* in una pagina delle funzioni principali, ad esempio forum, QnA e blog

   * segue tutte le attività per quella caratteristica generale

* per un post specifico, ad esempio un argomento forum, una domanda QnA o un articolo blog

   * segue tutte le attività per quella specifica voce

## Gestione delle impostazioni di notifica {#managing-notification-settings}

Selezionando il collegamento Impostazioni notifica dalla pagina Notifiche, è possibile per ciascun membro gestire il modo in cui vengono ricevute le notifiche.

Il canale Web è sempre abilitato.

![chlimage_1-244](assets/chlimage_1-244.png)

Il canale e-mail, che si basa sulla corretta [configurazione dell’e-mail](/help/communities/email.md), fornisce le stesse impostazioni del canale Web.

Il canale e-mail è disattivato per impostazione predefinita.

![chlimage_1-245](assets/chlimage_1-245.png)

Può essere attivata da un membro, ma dipende comunque dalla configurazione dell&#39;e-mail.

![chlimage_1-246](assets/chlimage_1-246.png)

## Visualizzazione delle notifiche {#viewing-notifications}

### Notifiche Web {#web-notifications}

Una [procedura guidata per la creazione di un sito](/help/communities/sites-console.md) community ora include un collegamento alla `Notifications` funzione nella barra dell&#39;intestazione del sito, sopra il banner. A differenza dei messaggi, le notifiche vengono create per ogni sito community, mentre i messaggi devono essere attivati durante il processo di creazione del sito.

Quando si visita il sito pubblicato, selezionando il `Notifications` collegamento vengono visualizzate tutte le notifiche relative al membro.

![chlimage_1-247](assets/chlimage_1-247.png)

### Notifiche e-mail {#email-notifications}

Quando il canale e-mail è abilitato, il membro riceve un messaggio e-mail contenente un collegamento al contenuto sul Web.

![chlimage_1-248](assets/chlimage_1-248.png)

## Personalizzare le notifiche e-mail {#customize-email-notifications}

Le organizzazioni possono personalizzare le notifiche e-mail [sovrapponendo](/help/communities/client-customize.md#overlays) i modelli in **/libs/settings/community/templates/email/html**.

Ad esempio, per modificare le menzioni notifiche e-mail (per un componente community) aggiungere una condizione** if **per la **menzione verbo** nei modelli dei componenti per i quali hai attivato il **supporto @menzioni** .

Per modificare il modello di notifiche e-mail per @Menzioni nei commenti del blog, posizionate fuori dalla casella in: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/it**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

