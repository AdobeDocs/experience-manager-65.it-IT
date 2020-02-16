---
title: Funzionalità Flussi attività
seo-title: Funzionalità Flussi attività
description: Attività di un membro della community che ha effettuato l'accesso
seo-description: Attività di un membro della community che ha effettuato l'accesso
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funzionalità Flussi attività{#activity-streams-feature}

## Introduzione {#introduction}

Le attività di un membro della comunità firmato, come l&#39;invio a un forum o blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi attraverso la configurazione del `Activity Streams` componente.

La possibilità di seguire aggiunge un&#39;altra visione delle attività quando i membri della comunità seguono i post di interesse o seguono le attività di altri membri della comunità.

Il documento descrive:

* aggiunta del componente Activity Streams a un sito AEM
* impostazioni di configurazione per il componente Activity Streams

### Aggiunta di flussi di attività a una pagina {#adding-activity-streams-to-a-page}

Se si desidera aggiungere un `Activity Streams` componente a una pagina in modalità di creazione, utilizzare il browser Componenti per individuare

* `Communities / Activity Streams`

e trascinatelo nella stessa posizione in una pagina in cui dovrebbero essere visualizzati i flussi di attività.

Per le informazioni necessarie, visita [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/essentials-activities.md#essentials-for-client-side) richieste, verrà visualizzato il `Activity Streams` componente:

![chlimage_1-24](assets/chlimage_1-24.png)

### Configurazione dei flussi di attività {#configuring-activity-streams}

Selezionate il `Activity Streams` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-25](assets/chlimage_1-25.png)

Nella scheda Attività **** utente, specificate le attività da visualizzare:

![chlimage_1-26](assets/chlimage_1-26.png)

* **Numero massimo di attività** il numero di attività da visualizzare

* **Percorso** risorsa flusso Lascia vuoto il campo predefinito per il sito community o il gruppo community. Il percorso della risorsa del flusso identifica l&#39;origine delle attività. Il valore predefinito è vuoto.

* **Visualizza visualizzazione** attività utente se questa opzione è selezionata, la pagina delle attività includerà una scheda che filtra le attività in base a quelle generate all&#39;interno della community dal membro corrente. Il valore predefinito è selezionato.

* **Visualizza la visualizzazione** Tutte le attività se selezionata, la pagina delle attività includerà una scheda che include tutte le attività generate all&#39;interno della comunità a cui il membro corrente ha accesso. Il valore predefinito è selezionato.

* **Visualizza visualizzazione** successiva se selezionata, la pagina delle attività includerà una scheda che filtra le attività in base a quelle che il membro corrente sta seguendo. Il valore predefinito è selezionato.

### Visualizzazione seguente {#following-view}

I componenti devono essere configurati per abilitare quanto segue. Le funzioni che consentono di seguire sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filibreria](/help/communities/file-library.md)[](/help/communities/comments.md), commenti.

![chlimage_1-27](assets/chlimage_1-27.png)

Il pulsante **Follow **fornisce un mezzo per seguire le voci come attività, [notifiche](/help/communities/notifications.md)o [iscrizioni](/help/communities/subscriptions.md). Ogni volta che il tasto **Follow **è selezionato, è possibile attivare o disattivare una selezione. La `Email Subscriptions` selezione è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **Seguente**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **Follow **I

* quando si visualizza il profilo di un altro membro
* in una pagina delle funzioni principali, ad esempio forum, QnA e blog

   * segue tutte le attività per quella caratteristica generale

* per un post specifico, ad esempio un argomento forum, una domanda QnA o un articolo blog

   * segue tutte le attività per quella specifica voce

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Activity Streams Essentials](/help/communities/essentials-activities.md) per gli sviluppatori.
